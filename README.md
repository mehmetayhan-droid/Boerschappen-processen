flowchart TD
    A[Boerschappen proces] --> B{Welke stroom?}

    B --> D2C[D2C boxen]
    B --> GH[Groothandel / Vitam]
    B --> DJI[DJI / gevangenissen]

    %% D2C
    subgraph D2C_FLOW [D2C boxen]
        D2C --> D2C1[Jaarafspraken met boeren]
        D2C1 --> D2C2[Team Culinair ontwikkelt recepten voor boxen]
        D2C2 --> D2C3{Zijn alle producten beschikbaar via jaarafspraken?}

        D2C3 -->|Ja| D2C5[Producten worden geleverd]
        D2C3 -->|Nee| D2C4[Ontbrekende producten inkopen bij boeren en/of groothandels]
        D2C4 --> D2C5

        D2C5 --> D2C6[Planning en verwerking in Excel en deels Odoo]
        D2C6 --> D2C7[Boxen packen op de Ijsvogel bij HQDC]
        D2C7 --> D2C8{Uitlevering naar consument}

        D2C8 --> D2C9[Pick up point]
        D2C8 --> D2C10[Trunkrs]
        D2C8 --> D2C11[Fietskoeriers]
        D2C8 --> D2C12[Boerschappen busjes]
    end

    %% Groothandel
    subgraph GH_FLOW [Groothandel / Vitam]
        GH --> GH1{Orderkanaal}
        GH1 -->|Boerschappen site| GH2[Verkooporder]
        GH1 -->|Apicbase| GH3[Automatische verkooporder in Odoo]

        GH2 --> GH4[Order in Odoo]
        GH3 --> GH4

        GH4 --> GH5[Cut off tijd 13:00]
        GH5 --> GH6{Zijn er voorverpakte of gesneden producten nodig?}

        GH6 -->|Nee| GH9[Picken via Odoo, scanners en productlijnen]
        GH6 -->|Ja| GH7[Voor 15:00 bestellen bij leverancier]
        GH7 --> GH8[Producten komen dezelfde dag binnen]
        GH8 --> GH9

        GH9 --> GH10[Producten op verschillende locaties picken]
        GH10 --> GH11[Extra producten op het einde toevoegen aan kratten]
        GH11 --> GH12[Orders packen]
        GH12 --> GH13[Orders verzenden naar distributielocaties]

        GH13 --> GH14{Distributielocatie}
        GH14 --> GH15[Breda HQ]
        GH14 --> GH16[Diemen]
        GH14 --> GH17[Kampen]

        GH13 --> GH18[Orderstroom naar NextUp]
        GH18 --> GH19[Routes maken voor drop off]
        GH19 --> GH20[Mogelijke pick up van inkooporders meenemen]
    end

    %% DJI
    subgraph DJI_FLOW [DJI / gevangenissen]
        DJI --> DJI1[14 locaties totaal]
        DJI1 --> DJI2{3 verschillende takken}

        DJI2 -->|Jeugd| DJI3[Koken met groep op locatie]
        DJI2 -->|Grootkeukens| DJI4[Graaf en Middelburg]
        DJI2 -->|Volwassen zelfstandig koken| DJI5[Maaltijden per persoon ingepakt]

        DJI3 --> DJI6[Rekensom maken voor benodigde producten]
        DJI4 --> DJI7[Grootverpakking berekenen]
        DJI5 --> DJI8[Maaltijden per persoon berekenen]

        DJI6 --> DJI9[Recepten weken van tevoren doorgestuurd]
        DJI7 --> DJI9
        DJI8 --> DJI9

        DJI9 --> DJI10[Recepten worden goedgekeurd]
        DJI10 --> DJI11[Bestellingen komen binnen via mail]
        DJI11 --> DJI12[Alles wordt verwerkt in Excel]

        DJI12 --> DJI13{3 Excel bestanden}
        DJI13 --> DJI14[Excel voor recepten]
        DJI13 --> DJI15[Excel voor berekening grootverpakking]
        DJI13 --> DJI16[Excel voor berekening maaltijden per persoon]

        DJI14 --> DJI17[Productbehoefte bepalen]
        DJI15 --> DJI17
        DJI16 --> DJI17

        DJI17 --> DJI18[Producten inkopen]
        DJI18 --> DJI19[Producten apart leggen voor DJI klant]
        DJI19 --> DJI20[Producten invoeren in OutSystems]
        DJI20 --> DJI21[Producten packen op de Ijsvogel]
        DJI21 --> DJI22[DJI orders verzendklaar maken]
        DJI22 --> DJI23[Verzending via vervoerder]
        DJI23 --> DJI24[Levering aan DJI locaties]
    end

    %% Systemen
    D2C6 -.-> SYS1[Excel]
    D2C6 -.-> SYS2[Odoo]

    GH3 -.-> SYS3[Apicbase]
    GH4 -.-> SYS2
    GH9 -.-> SYS2
    GH18 -.-> SYS4[NextUp]

    DJI12 -.-> SYS1
    DJI20 -.-> SYS5[OutSystems]
