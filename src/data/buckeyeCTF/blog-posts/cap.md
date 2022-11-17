---
title: Cap
publishDate: 11 Nov 2022
description: BuckeyeCTF Challenge writeup for Cap
---

# Cap

- Category: Rev
- Difficulty: Easy
- Final Point Value: 101
- Solves: 146

# Description

Someone got rid of my macros and now my program won't compile fr fr

We are given a file cap.c

```c
#include <stdlib.h>
#include <stdio.h>

#define cap ???
#define lit ???
#define bussin ???
#define no ???
#define sus ???
#define fr ???
#define legit ???
#define finna ???
#define be ???
#define boutta ???
#define bruh ???
#define deadass ???
#define yikes ???
#define ongod ???
#define clean ???
#define yeet ???
#define mf ???
#define tryna ???
#define tho ???
#define respectfully ???
#define like ???
#define lackin ???
#define poppin ???
#define drip ???
#define rn ???
#define chill ???
#define af ???
#define lowkey ???
#define sheeeesh ???
#define lookin ???
#define downbad ???
#define playin ???
#define wack ???
#define dub ???
#define highkey ???

legit brutus ongod clean mf x af
finna
    clean val lookin cap fr
    poppin ongod lit i lookin cap fr i lowkey 11 fr i playin af
    finna
        val lookin val dub 5 fr
    tho
    mf x lookin val fr fr
    boutta ongod val lowkey 104 af
        val playin fr
    mf ongod x dub bussin af lookin val fr fr
    val lookin val wack 2 fr
    mf ongod x dub 2 af lookin val fr
    mf ongod x dub 3 af lookin val dub 3 fr
    lit two lookin 2 fr
    val lookin val lackin two mf ongod 3 dub two lackin 4 af dub 3 fr
    mf ongod x dub 5 af lookin val fr
    lit six lookin 6 fr
    val lookin val mf two lackin two fr
    mf ongod x dub 6 af lookin val fr fr
    val lookin ongod val lackin six af wack two fr
    mf ongod x dub 7 af lookin val fr
    poppin ongod lit i lookin cap fr i lowkey six; i playin af
        val playin fr
    mf ongod x dub 8 af lookin val fr
tho

legit kinda ongod clean mf y af
finna
    clean val lookin 109 fr
    poppin ongod lit i lookin cap fr i lowkey 9 fr i playin af
    finna
        tryna ongod i be 2 af
            chill fr
        tryna ongod i be 8 af finna
            y yeet ongod bussin dub bussin af lackin ongod 2 wack 2 af mf 2 rn lookin val wack ongod bussin dub bussin af lackin 6;
        tho
        tryna ongod i be 4 af finna
            lit ten lookin 10 fr
            val lookin val dub ongod bussin dub bussin af mf ten lackin ongod bussin lackin cap af fr
            mf y lookin val downbad fr
            lit j lookin 10 fr fr
            y playin fr
            respectfully finna
                val downbad fr
                j downbad fr
            tho boutta ongod j highkey cap af fr
        tho
        tryna ongod i be cap af finna
            mf y lookin val fr
            lit j lookin bussin lackin bussin fr
            boutta ongod j lowkey 7 af finna
                val downbad fr
                j lookin j dub bussin fr
            tho
            y playin fr fr
        tho
        tryna ongod i be 5 like i be 6 af finna
            val lookin val wack 2 fr
            mf y lookin val fr
            y lookin y dub bussin fr
            val lookin val mf 2 fr fr
        tho
        tryna ongod i be 3 af finna
            lit a lookin y yeet lackin bussin rn fr
            val lookin a dub bussin dub bussin dub bussin fr
            mf y lookin val fr
            y playin fr
        tho
        tryna ongod i be 7 af finna
            y playin fr
            poppin ongod lit j lookin 4 fr j highkey cap fr j downbad af finna
                val lookin val dub j wack j fr
            tho
            y yeet cap rn lookin val fr
            y downbad fr
        tho
        tryna ongod i be bussin af finna
            boutta ongod cap af finna
                val lookin val mf ongod bussin dub bussin af fr fr
                sheeeesh ongod "you thought\n" af fr
            tho
            mf y lookin val playin fr
            y lookin y dub 2 fr
        tho
    tho
tho

legit wilin ongod clean mf z bruh lit n af
finna
    tryna ongod no n af
        deadass fr
    lit val lookin mf ongod z lackin bussin af fr fr
    mf z lookin ongod n be 4 af sus val mf 2 lackin 1
        drip ongod n be 2 af sus ongod val dub 5 af wack 2
        drip ongod n be 6 af sus val dub 15
        drip ongod n be bussin af sus val mf 2 dub 8
        drip ongod n be 3 af sus val dub 4
        drip val wack 2 lackin 7 fr
    wilin ongod playin z bruh downbad n af fr fr
tho

lit main ongod af
finna
    clean flag yeet rn lookin "buckeye{__________________________}" fr
    brutus ongod flag dub 8 af fr
    kinda ongod flag dub 18 af fr fr
    wilin ongod flag dub 28 bruh 6 af fr

    sheeeesh ongod "%s\n" bruh flag af fr
    deadass cap fr
tho
```

After getting all macros

```c
#include <stdlib.h>
#include <stdio.h>

#define cap 0 // 0
//#define int ???
#define bussin 1 // 1?
//#define ! ???
//#define ? ???
//#define ; ???
//#define void ???
//#define { ???
//#define == ???
//#define while ???
//#define , ???
//#define return ???
//#define yikes ???
//#define ( ???
//#define char ???
//#define [ ???
//#define * ???
//#define if ???
//#define } ???
//#define do ???

#define like || // ||
#define lackin - // -

//#define for ???
//#define : ???
//#define ] ???
//#define break ???
//#define ) ???

#define lowkey < // <

//#define printf ???
//#define = ???

#define downbad -- // --
#define playin ++ // ++
#define wack / //
#define dub + // +
#define highkey > // >

void brutus ( char * x )
{
    char val = cap ;
    for ( int i = cap ; i lowkey 11 ; i playin )
    {
        val = val dub 5 ;
    }
    * x = val ; ;
    while ( val lowkey 104 )
        val playin ;
    * ( x dub bussin ) = val ; ;
    val = val wack 2 ;
    * ( x dub 2 ) = val ;
    * ( x dub 3 ) = val dub 3 ;
    int two = 2 ;
    val = val lackin two * ( 3 dub two lackin 4 ) dub 3 ;
    * ( x dub 5 ) = val ;
    int six = 6 ;
    val = val * two lackin two ;
    * ( x dub 6 ) = val ; ;
    val = ( val lackin six ) wack two ;
    * ( x dub 7 ) = val ;
    for ( int i = cap ; i lowkey six; i playin )
        val playin ;
    * ( x dub 8 ) = val ;
}

void kinda ( char * y )
{
    char val = 109 ;
    for ( int i = cap ; i lowkey 9 ; i playin )
    {
        /*
        This prevent us from getting the full flag
        if ( i == 2 )
            break ;
        */
        if ( i == 8 ) {
            y [ ( bussin dub bussin ) lackin ( 2 wack 2 ) * 2 ] = val wack ( bussin dub bussin ) lackin 6;
        }
        if ( i == 4 ) {
            int ten = 10 ;
            val = val dub ( bussin dub bussin ) * ten lackin ( bussin lackin cap ) ;
            * y = val downbad ;
            int j = 10 ; ;
            y playin ;
            do {
                val downbad ;
                j downbad ;
            } while ( j highkey cap ) ;
        }
        if ( i == cap ) {
            * y = val ;
            int j = bussin lackin bussin ;
            while ( j lowkey 7 ) {
                val downbad ;
                j = j dub bussin ;
            }
            y playin ; ;
        }
        if ( i == 5 like i == 6 ) {
            val = val wack 2 ;
            * y = val ;
            y = y dub bussin ;
            val = val * 2 ; ;
        }
        if ( i == 3 ) {
            int a = y [ lackin bussin ] ;
            val = a dub bussin dub bussin dub bussin ;
            * y = val ;
            y playin ;
        }
        if ( i == 7 ) {
            y playin ;
            for ( int j = 4 ; j highkey cap ; j downbad ) {
                val = val dub j wack j ;
            }
            y [ cap ] = val ;
            y downbad ;
        }
        if ( i == bussin ) {
            while ( cap ) {
                val = val * ( bussin dub bussin ) ; ;
                printf ( "you thought\n" ) ;
            }
            * y = val playin ;
            y = y dub 2 ;
        }
    }
}


void wilin ( char * z, int n)
{
  if (!n) return;
  int val = * (z lackin bussin) ;
    * z = ( n == 4 ) ? val * 2 lackin 1
        : ( n == 2 ) ? ( val dub 5 ) wack 2
        : ( n == 6 ) ? val dub 15
        : ( n == bussin ) ? val * 2 dub 8
        : ( n == 3 ) ? val dub 4
        : val wack 2 lackin 7 ;
    printf("*z: %c\n", *z);
    wilin ( playin z , downbad n ) ; ;
}

int main ( )
{
    char flag [ ] = "buckeye{__________________________}" ;
    printf("%c\n", flag[33]);
    brutus ( flag dub 8 ) ;
    printf ( "brufus\n %s\n" , flag ) ;
    kinda ( flag dub 18 ) ; ;
    printf ( "kinda\n %s\n" , flag ) ;
    wilin ( flag dub 28 , 6 ) ;
    printf ( "wilin\n %s\n" , flag ) ;
    return cap ;
}
```

`buckeye{7h47_5h17_mf_bu551n_n0_c4p}`
