---
title: Soda
publishDate: 11 Nov 2022
description: BuckeyeCTF Challenge writeup
---

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.util.Scanner;

public class soda {
    static final int NUM_DRINKS = 12;
    static boolean bystanders = false;
    static float wallet = 500.0F;

    public soda() {
    }

    public static void main(String[] var0) {
        VendingMachine var1 = new VendingMachine();
        Scanner var2 = new Scanner(System.in);
        System.out.println("\nThe prophecy states that worthy customers receive flags in their cans...");

        while(true) {
            System.out.println("\n" + var1);
            System.out.println(String.format("I have $%.02f in my wallet", wallet));
            System.out.print("command> ");

            try {
                String var3 = var2.nextLine();
                if (var3.isEmpty()) {
                    break;
                }

                String[] var4 = var3.split(" ");
                processCommand(var1, var4);
            } catch (Exception var5) {
                break;
            }
        }

        System.out.println();
        var2.close();
    }

    private static void processCommand(VendingMachine var0, String[] var1) {
        if (var1[0].equalsIgnoreCase("help")) {
            System.out.println(">> You're telling me you don't know how to use a vending machine?");
        } else {
            int var6;
            if (var1[0].equalsIgnoreCase("purchase")) {
                if (var1.length > 1) {
                    try {
                        var6 = Integer.parseInt(var1[1]);
                        if (var6 >= 1 && var6 <= 12) {
                            var0.buy(var6 - 1);
                        } else {
                            throw new RuntimeException();
                        }
                    } catch (Exception var4) {
                        System.out.println(">> That's not a real choice");
                    }
                } else {
                    System.out.println(">> Purchase what?");
                }
            } else if (var1[0].equalsIgnoreCase("punch")) {
                System.out.println(">> That's not a good idea");
            } else if (var1[0].equalsIgnoreCase("kick")) {
                System.out.println(">> That's a terrible idea");
            } else if (var1[0].equalsIgnoreCase("shake")) {
                System.out.println(">> That's the worst idea ever");
            } else if (var1[0].equalsIgnoreCase("shatter")) {
                System.out.println(">> What is wrong with you???");
            } else if (var1[0].equalsIgnoreCase("reach")) {
                if (bystanders) {
                    System.out.println(">> I can't do that with people around!\n>> They'll think I'm stealing!");
                } else {
                    var6 = var0.reach();
                    var0.dropped += var6;
                    if (var6 > 0) {
                        System.out.println(">> Ok, here goes... gonna reach through the door and try to knock it down...");
                        pause(3);
                        System.out.println(">> !!! I heard something fall!");
                    } else {
                        System.out.println(">> There's nothing to reach for");
                    }

                }
            } else if (var1[0].equalsIgnoreCase("wait")) {
                boolean var2 = false;

                try {
                    var6 = Integer.parseInt(var1[1]);
                } catch (Exception var5) {
                    System.out.println(">> Not sure what you mean");
                    return;
                }

                pause(var6);
                if (var6 >= 10) {
                    bystanders = false;
                    System.out.println(">> ...Looks like nobody's around...");
                } else {
                    bystanders = true;
                    System.out.println(">> People are walking down the street.");
                }

            } else if (var1[0].equalsIgnoreCase("tap")) {
                System.out.println(">> Tapping the glass is harmless, right?");
                pause(1);
                var0.tap();
                System.out.println(">> Not sure if that helped at all...");
            } else if (var1[0].equalsIgnoreCase("grab")) {
                if (var0.dropped > 0) {
                    System.out.println(">> Alright!! Let's see what I got!");
                    var0.retrieve();
                } else {
                    System.out.println(">> There's nothing to grab...");
                }

            } else {
                System.out.println(">> Not sure what you mean");
            }
        }
    }

    private static void printFlag() {
        try {
            BufferedReader var0 = new BufferedReader(new FileReader("flag.txt"));
            System.out.println(">> WOAH!! There's a flag in here!!");

            String var1;
            while((var1 = var0.readLine()) != null) {
                System.out.println(var1);
            }
        } catch (Exception var2) {
            System.out.println(">> You find a piece of paper in the can! It reads:");
            System.out.println("\n\t\"You are not worthy\"\n");
        }

    }

    private static void pause(int var0) {
        try {
            for(int var1 = 0; var1 < var0; ++var1) {
                System.out.print(". ");
                Thread.sleep(1000L);
            }
        } catch (Exception var2) {
        }

        System.out.println();
    }

    static class Drink {
        float cost = (float)(Math.random() * 6.0);
        DrinkStatus status;
        int stuck;

        public Drink() {
            this.status = Math.random() > 0.75 ? soda.Drink.DrinkStatus.EMPTY : soda.Drink.DrinkStatus.READY;
            this.stuck = 3;
        }

        public String getCostLabel() {
            return String.format("%1.02f", this.cost);
        }

        public String[] asText(int var1) {
            String[] var2 = new String[]{"| " + var1 + (var1 < 10 ? "    " : "   "), "|      ", "|      ", "|      ", "|      ", "| " + this.getCostLabel() + " "};
            if (this.status != soda.Drink.DrinkStatus.EMPTY && this.status != soda.Drink.DrinkStatus.DROPPED) {
                String[] var3 = new String[]{"| " + var1 + (var1 < 10 ? "    " : "   "), "|  __  ", this.status == soda.Drink.DrinkStatus.STUCK ? "| |**| " : "| |  | ", "| |__| ", "|      ", "| " + this.getCostLabel() + " "};
                return var3;
            } else {
                return var2;
            }
        }

        static enum DrinkStatus {
            EMPTY,
            READY,
            STUCK,
            DROPPED;

            private DrinkStatus() {
            }
        }
    }

    static class VendingMachine {
        Drink[] drinks = new Drink[12];
        public int dropped = 0;

        public VendingMachine() {
            for(int var1 = 0; var1 < 12; ++var1) {
                this.drinks[var1] = new Drink();
            }

        }

        public boolean hasDroppedDrinks() {
            for(int var1 = 0; var1 < 12; ++var1) {
                if (this.drinks[var1].status == soda.Drink.DrinkStatus.DROPPED) {
                    return true;
                }
            }

            return false;
        }

        public void buy(int var1) {
            if (this.drinks[var1].status != soda.Drink.DrinkStatus.READY) {
                System.out.println(">> [OUT OF STOCK]");
            } else if (soda.wallet > this.drinks[var1].cost) {
                System.out.println(">> [VENDING]");
                soda.pause(5);
                System.out.println(">> ...Wait... IT'S STUCK?? NOOOOOO");
                this.drinks[var1].status = soda.Drink.DrinkStatus.STUCK;
                soda.wallet -= this.drinks[var1].cost;
            } else {
                System.out.println(">> I don't have enough money :(");
            }
        }

        public void tap() {
            for(int var1 = 0; var1 < 12; ++var1) {
                if (this.drinks[var1].status == soda.Drink.DrinkStatus.STUCK && this.drinks[var1].stuck > 0) {
                    --this.drinks[var1].stuck;
                }
            }

        }

        public int reach() {
            int var1 = 0;

            for(int var2 = 0; var2 < 12; ++var2) {
                if (this.drinks[var2].status == soda.Drink.DrinkStatus.STUCK && this.drinks[var2].stuck == 0) {
                    this.drinks[var2].status = soda.Drink.DrinkStatus.DROPPED;
                    ++var1;
                }
            }

            return var1;
        }

        public void retrieve() {
            int var1 = -1;
            float var2 = -1.0F;

            // The algorithm in question
            for(int var3 = 0; var3 < 12; ++var3) {
                if (this.drinks[var3].status != soda.Drink.DrinkStatus.EMPTY && this.drinks[var3].cost > var2) {
                    var1 = var3;
                    var2 = this.drinks[var3].cost;
                }
            }



            System.out.println(var1);
            System.out.println(var2);
            if (this.drinks[var1].status == soda.Drink.DrinkStatus.DROPPED) {
                // print the drink associated with var1
                soda.printFlag();
            } else {
                System.out.println(">> No flags in here... was the prophecy a lie...?");
                // print the drink associated with var1
                System.out.println(this.drinks[var1].getCostLabel());

            }

        }

        public String toString() {
            String var1 = "-------".repeat(6) + "-\n";

            int var2;
            int var3;
            for(var2 = 0; var2 < 6; ++var2) {
                for(var3 = 0; var3 < 6; ++var3) {
                    var1 = var1 + this.drinks[var3].asText(var3 + 1)[var2];
                }

                var1 = var1 + "|\n";
            }

            var1 = var1 + "-------".repeat(6) + "-\n";

            for(var2 = 0; var2 < 6; ++var2) {
                for(var3 = 6; var3 < 12; ++var3) {
                    var1 = var1 + this.drinks[var3].asText(var3 + 1)[var2];
                }

                var1 = var1 + "|\n";
            }

            var1 = var1 + "-------".repeat(6) + "-\n";
            return var1;
        }
    }
}
```
