# utl-doblebook-hotel-and-same-guest-booked--hotel-same-day-in-different-years-sql-wps-r-py
Doublebook hotel and same guest booked  hotel same day in different years sql wps r py
    %let pgm=utl-doblebook-hotel-and-same-guest-booked--hotel-same-day-in-different-years-sql-wps-r-py;

    Doublebook hotel and same guest booked  hotel same day in different years sql wps r py

    Yhis type of probem is best done using a wps datastep (first dot & last dot)
    SQL does not like to keep conditional duplicate groups (often defaults to one record for various dup groups).

      SOLUTION

         1 wps sort nouniquekey (just duplcate bookings on same day - dup groups)
            proc sort data=sd1.have out=sd1.want nouniquekey;
            by year day hotel_guest;
         2 wps sql (SAMEYEAR & DIFYEAR)
         3 wps r sql
         4 wps python sql


    github
    https://tinyurl.com/yv4sbex2
    https://github.com/rogerjdeangelis/utl-doblebook-hotel-and-same-guest-booked--hotel-same-day-in-different-years-sql-wps-r-py

    github csv input
    https://tinyurl.com/46zj2ej5
    https://raw.githubusercontent.com/rogerjdeangelis/utl-doblebook-hotel-and-same-guest-booked--hotel-same-day-in-different-years-sql-wps-r-py/main/have.csv

    related to
    https://tinyurl.com/4za7xfa8
    https://stackoverflow.com/questions/77594245/how-to-find-out-if-two-people-book-the-same-hotel-on-the-same-day-more-than-once


    /**************************************************************************************************************************/
    /*                                     |                                                                                  */
    /* There are only 2 hotels in the input|                                                                                  */
    /* City Hotel    = C_                  |                                                                                  */
    /* Resort Hotel  = R_                  |                                                                                  */
    /*                                     |            DOUBLE BOOKINGS                   SAME GUEST DIFFERENT YEARS          */
    /*    _                   _            |              _               _     _                _               _     ____   */
    /*   (_)_ __  _ __  _   _| |_          |   ___  _   _| |_ _ __  _   _| |_  / |    ___  _   _| |_ _ __  _   _| |_  |___ \  */
    /*   | | `_ \| `_ \| | | | __|         |  / _ \| | | | __| `_ \| | | | __| | |   / _ \| | | | __| `_ \| | | | __|   __) | */
    /*   | | | | | |_) | |_| | |_          | | (_) | |_| | |_| |_) | |_| | |_  | |  | (_) | |_| | |_| |_) | |_| | |_   / __/  */
    /*   |_|_| |_| .__/ \__,_|\__|         |  \___/ \__,_|\__| .__/ \__,_|\__| |_|   \___/ \__,_|\__| .__/ \__,_|\__| |_____| */
    /*           |_|                       |                 |_|                                    |_|                       */
    /*                                     |                                                                                  */
    /* YEAR     DAY     HOTEL_GUEST        | YEAR    DAY   HOTEL_GUEST     STATUS   YEAR     DAY   HOTEL_GUEST    STATUS      */
    /*                                     |                                                                                  */
    /*  16     27APR    R_JordanBerg       |  17    02JAN  R_MatthewLee   SAMEYEAR   15     01JUL  C_MrRobert     DIFYEAR     */
    /*  15     13JUL    R_ShannonWilcox    |  17    02JAN  R_MatthewLee   SAMEYEAR   16     01JUL  C_MrRobert     DIFYEAR     */
    /*  15     14JUL    R_JamesCobb        |                                                                                  */
    /*  15     07AUG    R_JasonAnderson    |  16    03DEC  R_Jennifer     SAMEYEAR   17     03JUL  C_JenniferJohn DIFYEAR     */
    /*  15     18AUG    R_MichelleSmith    |  16    03DEC  R_Jennifer     SAMEYEAR   16     03JUL  C_JenniferJohn DIFYEAR     */
    /*  15     02OCT    R_DanielleMendoza  |                                                                                  */
    /*  15     19OCT    R_MonicaAllen      |  15    05DEC  C_RobertLee    SAMEYEAR   16     04OCT  C_MichaelScott DIFYEAR     */
    /*  15     23OCT    R_JosephFoster     |  15    05DEC  C_RobertLee    SAMEYEAR   15     04OCT  C_MichaelScott DIFYEAR     */
    /*  15     05DEC    R_AngelaGrant      |                                                                                  */
    /*  15     30DEC    R_TaylorLutz       |  16    06APR  C_NicoleKlein  SAMEYEAR   16     04OCT  C_MrMichael    DIFYEAR     */
    /*  16     24MAR    R_TaylorShea       |  16    06APR  C_NicoleKlein  SAMEYEAR   15     04OCT  C_MrMichael    DIFYEAR     */
    /*  16     14MAY    R_AngelChen        |                                                                                  */
    /*  16     21JUN    R_GregoryYoung     |  17    06JUL  C_AngelWhite   SAMEYEAR   17     05AUG  C_DavidSmith   DIFYEAR     */
    /*  16     22JUN    R_SuzanneDavis     |  17    06JUL  C_AngelWhite   SAMEYEAR   15     05AUG  C_DavidSmith   DIFYEAR     */
    /*  16     22JUN    R_SuzanneDavis     |                                                                                  */
    /*  16     04JUL    R_TylerKaiser      |  17    06JUL  C_KellySmith   SAMEYEAR                                            */
    /*  16     29AUG    R_MariaHunter      |  17    06JUL  C_KellySmith   SAMEYEAR                                            */
    /*  17     27APR    R_JenniferSmith    |                                                                                  */
    /*  16     21JUN    R_GregoryYoung     |  16    07MAR  C_LaurenDavis  SAMEYEAR                                            */
    /*  17     07MAR    R_MichaelFerguson  |  16    07MAR  C_LaurenDavis  SAMEYEAR                                            */
    /*  17     02JUL    R_CalebSnow        |                                                                                  */
    /*  15     11OCT    R_AlyssaGordon     |                                                                                  */
    /*  16     27APR    R_JenniferSmith    |                                                                                  */
    /*  17     22FEB    R_ChristineBarrett |                                                                                  */
    /*  16     27APR    R_JordanBerg       |                                                                                  */
    /*                                     |                                                                                  */
    /**************************************************************************************************************************/


    options validvarname=upcase;
    libname sd1 "d:/sd1";

    data sd1.have;
      informat year $2. day $5. hotel_guest $33.;
      input year day hotel_guest @@;
    cards4;
    15 13JUL R_ShannonWilcox 15 14JUL R_JamesCobb 15 07AUG R_JasonAnderson 15 18AUG R_MichelleSmith 15 02OCT
    R_DanielleMendoza 15 19OCT R_MonicaAllen 15 23OCT R_JosephFoster 15 05DEC R_AngelaGrant 15 30DEC R_TaylorLutz 16 24MAR
    R_TaylorShea 16 14MAY R_AngelChen 16 21JUN R_GregoryYoung 16 22JUN R_SuzanneDavis 16 22JUN R_SuzanneDavis 16 04JUL
    R_TylerKaiser 16 29AUG R_MariaHunter 17 27APR R_JenniferSmith 16 21JUN R_GregoryYoung 17 07MAR R_MichaelFerguson 17
    02JUL R_CalebSnow 15 11OCT R_AlyssaGordon 16 27APR R_JenniferSmith 17 22FEB R_ChristineBarrett 16 27APR R_JordanBerg 15
    22JUL R_AlanWest 15 17JUL R_MichaelSmith 15 13AUG R_TammyDuncan 15 18AUG R_KylePowell 15 26AUG R_JoshuaLarsen 15 24AUG
    R_RogerTrevino 15 15SEP R_BrittanyBailey 15 19SEP R_NicholasJones 15 20SEP R_LindaElliott 15 01OCT R_AmandaBond 17 09MAR
    R_CarolynConner 15 06OCT R_MarkBrown 15 11OCT R_ChristopherMoore 15 15OCT R_NicoleDavis 15 20OCT R_RachaelMills 15 22OCT
    R_TimothyTaylor 16 04MAY R_MicheleOchoa 15 02NOV R_DonnaManning 16 08JUN R_BobbyMiller 16 11DEC R_ScottHolden 15 19NOV
    R_RandyFrye 15 24NOV R_MrsSarah 16 07MAR R_AntonioBrown 15 28DEC R_WilliamPatton 15 30DEC R_DavidEdwards 17 02JAN
    R_MatthewLee 16 15JAN R_JuanWagner 16 19JAN R_ChristineCollins 16 22JAN R_StevenHerring 16 05FEB R_DanielMason 16 11APR
    R_MatthewMorrow 16 13FEB R_TammyNelson 16 12FEB R_JacobRamos 16 11APR R_MichelleGaines 16 04MAR R_MarkSmith 16 04MAR
    R_MarcusMiranda 16 05MAR R_MelissaRice 16 07MAR R_MichaelFerguson 16 13MAR R_SarahStone 16 09MAR R_MrsAnna 16 13MAR
    R_SeanThomas 16 19MAR R_AndreaThomas 16 15MAR R_JackieLewis 16 07APR R_AnthonyHarper 16 09APR R_MrAnthony 16 10APR
    R_DarinHernandez 16 19APR R_BarryTerry 16 24APR R_StephanieRodgers 16 27APR R_JessicaBrown 16 28APR R_AaronHorton 16
    27APR R_JuliaEstes 16 30APR R_KylePerry 16 11MAY R_KathyFowler 16 06OCT R_ShawnStewart 16 18MAY R_StevenRichards 16
    19MAY R_JamieJohnston 16 24MAY R_CarmenGrant 16 26MAY R_LindaReed 16 25MAY R_BonnieMcdaniel 17 10MAR R_CodyTaylor 16
    21JUN R_FrancesHiggins 16 27JUN R_MaryDavis 16 27JUN R_MaryDavis 16 27JUN R_RobertBrandt 16 07JUL R_EileenManning 16
    09JUL R_WilliamAnderson 16 24JUL R_AngelaJohnson 16 02AUG R_VincentDunn 16 05AUG R_ShaneThomas 16 18AUG R_AndreaSmith 16
    15AUG R_AprilFields 16 18AUG R_MichelleSmith 16 18AUG R_KylePowell 16 22AUG R_MargaretWilliams 16 28AUG R_KarenHendricks
    16 01SEP R_NicoleHall 16 29AUG R_MariaHunter 16 24SEP R_ScottPetty 16 19SEP R_NicholasJones 16 27SEP R_MrsJennifer 16
    06OCT R_MarkBrown 16 05OCT R_TamaraRhodes 16 06OCT R_ThomasGuerra 16 17OCT R_LoriYoung 16 20OCT R_KariKim 16 24OCT
    R_BradleyRodriguez 16 23OCT R_JosephFoster 16 24OCT R_GeorgeWilson 16 22OCT R_TimothyTaylor 16 21OCT R_CharlesWalls 16
    29OCT R_JenniferAdkins 16 24OCT R_KellyQuinn 16 29OCT R_LisaRichardson 16 29OCT R_LisaRichardson 16 01DEC R_AshleyHester
    16 30NOV R_DavidDay 16 03DEC R_JenniferCarlson 16 03DEC R_JenniferCarlson 16 10DEC R_AmyWalker 16 07DEC R_MarkWood 16
    15DEC R_WilliamRuiz 16 22DEC R_AndreaFlynn 17 03JAN R_MelissaWright 17 04JAN R_RaymondMurray 17 02JAN R_MatthewLee 17
    07JAN R_PatrickLowery 17 12JAN R_JacquelineBlackwell 17 16JAN R_JasonHanson 17 16JAN R_JasonHanson 17 27JAN R_MrCalvin
    17 15MAY R_EricaPalmer 17 13FEB R_TammyNelson 17 18FEB R_StephanieVasquez 17 21FEB R_GrantHarding 17 28FEB
    R_AllisonRoberts 17 23FEB R_KevinDavis 17 20FEB R_KathySnyder 17 03MAY R_AlexandraJohnson 17 02MAR R_CarlaParker 17
    15FEB R_KristinaBoyd 17 13MAR R_SeanThomas 17 20MAR R_CassandraBrooks 17 31MAR R_RobinMontoya 17 01APR R_JesseMorales 17
    09APR R_MrAnthony 17 08APR R_MichelleWagner 17 14APR R_MichaelMccann 17 17APR R_JasminePayne 17 16APR R_AmberDavis 17
    15APR R_ShawnaWolfe 17 16APR R_AmberDavis 17 25APR R_ScottBruce 17 22APR R_KaylaBennett 17 29APR R_SharonHansen 17 14MAY
    R_AnitaCampbell 17 02JUN R_SamuelHernandez 17 11JUN R_CassandraDixon 17 16JUN R_DavidMoore 17 16JUN R_DavidMoore 17
    24JUN R_RichardTate 17 04JUL R_DebraVargas 17 11JUL R_JuliaHouse 17 17JUL R_MichaelSmith 17 30JUL R_DouglasBrown 17
    30JUL R_DouglasBrown 17 15AUG R_DavidJohnson 17 20AUG R_JeremyTran 15 25JUL C_RichardParsons 15 01AUG C_DianeCarpenter
    15 05AUG C_DavidSmith 15 06AUG C_TiffanySmith 15 13AUG C_AshleyBaldwin 15 14AUG C_MichaelWilliams 15 17AUG
    C_DouglasJacobs 15 23AUG C_AaronRivers 15 25AUG C_DustinWilliams 15 01SEP C_RyanStewart 15 07SEP C_JasonDouglas 15 18SEP
    C_KaitlynSmith 15 21SEP C_ElizabethByrd 15 25SEP C_RobertBarry 15 02OCT C_JohnYates 15 04OCT C_MichaelScott 15 04OCT
    C_MrMichael 15 09OCT C_SuzanneDiaz 15 15OCT C_LisaJones 15 25OCT C_ElizabethCohen 15 28OCT C_DanielHamilton 15 28OCT
    C_PeggyWade 15 15NOV C_CourtneyHuerta 15 18NOV C_CarolBarnes 15 30DEC C_GarrettHayes 16 15JAN C_TammySmith 16 18JAN
    C_DavidMoore 16 27JAN C_KellyHoffman 16 04FEB C_CharlesGarcia 16 17MAR C_ChristopherGreen 16 17MAR C_ChristopherGreen 16
    06APR C_NicoleKlein 16 18MAY C_RobinSmith 16 26MAY C_MaryJohnson 16 26MAY C_PedroSexton 16 26MAY C_MaryJohnson 16 26MAY
    C_JohnFox 16 26MAY C_TracyWilliams 16 09JUN C_ChristopherJones 16 01JUL C_TroyIngram 16 23SEP C_NancyStrong 15 01JUL
    C_MrRobert 15 04JUL C_MollyHutchinson 15 08JUL C_CatherineDominguez 16 10APR C_JohnSoto 15 21SEP C_LauraGuerrero 15
    22SEP C_JulieGray 15 22SEP C_JulieGray 15 21SEP C_EricRosales 15 05OCT C_DanaSmith 15 09OCT C_DebbieNichols 15 12OCT
    C_JeffreyCannon 15 15OCT C_GeorgeRodriguez 15 15OCT C_LisaJones 15 16OCT C_KelseyCraig 15 19NOV C_ChristopherMoore 15
    19NOV C_ChristopherMoore 16 30JAN C_MichaelRodriguez 15 05DEC C_RobertLee 15 05DEC C_KatieSmith 15 05DEC C_RobertLee 17
    03JAN C_CharleneMejia 15 29DEC C_HaydenSharp 16 02JAN C_MrsKaren 16 02JAN C_RobertMedina 16 16JAN C_RebeccaDiaz 17 17MAY
    C_MaryPoole 16 20JAN C_MariaDelgado 16 25JAN C_JeanetteCollins 16 27JAN C_KellyHoffman 16 29JAN C_AngelaHernandez 16
    05FEB C_JamesLopez 16 06FEB C_DonBush 16 26FEB C_AnthonyLewis 16 02MAR C_AlejandroAnderson 16 07MAR C_LawrenceMata 16
    07MAR C_LaurenDavis 16 07MAR C_LaurenDavis 16 11MAR C_MatthewParker 16 11MAR C_ElizabethThomas 16 11MAR C_ShellyMejia 16
    22MAR C_SarahAguilar 16 28MAR C_DarrylScott 16 31MAR C_KellyBurns 16 02APR C_RobertBrown 16 06APR C_NicoleKlein 16 04APR
    C_WilliamJacobs 16 08APR C_JulieHicks 16 15APR C_JohnHall 16 15APR C_JohnHall 16 14APR C_ChristopherPreston 16 14APR
    C_DeborahGraham 16 18APR C_SamanthaCunningham 16 09APR C_DeborahWaters 16 17APR C_ChristopherWilliams 16 23APR
    C_AnaMyers 16 25APR C_NathanNewman 16 26APR C_BryanGilmore 16 28APR C_SarahGibson 16 05MAY C_ArthurLuna 16 28APR
    C_RodneyCobb 16 12OCT C_JeffreyCannon 16 12MAY C_OscarSchroeder 16 22MAY C_PennyWang 16 24MAY C_JacobWashington 16 24MAY
    C_CherylLewis 16 26MAY C_TracyWilliams 16 30MAY C_JamesSanders 16 29MAY C_GinaSmith 16 29MAY C_AlexandraBrown 16 03JUN
    C_LisaJones 16 11JUN C_DavidBernard 16 09JUN C_ChristopherJones 16 15JUN C_KimberlyRodriguez 16 17JUN C_DaisyJones 16
    17JUN C_RobinLopez 16 18JUN C_JulieCrosby 16 22JUN C_PhillipReyes 16 24JUN C_ZacharyCruz 16 24JUN C_NatashaGuerra 16
    24JUN C_JamesCole 16 26JUN C_ChristopherAllen 16 30JUN C_StevenArmstrong 16 30JUN C_StevenArmstrong 16 01JUL C_MrRobert
    16 05JUL C_MichaelGarcia 16 30JUN C_CoreyTucker 16 04JUL C_JenniferNelson 16 03JUL C_JenniferJohnson 16 08JUL
    C_CatherineDominguez 16 08JUL C_TiffanyAllen 16 09JUL C_TheresaParsons 16 11JUL C_KimberlyRoberts 17 05MAR
    C_DerekGriffith 16 11JUL C_KimberlyRoberts 16 13JUL C_TeresaGoodwin 16 17JUL C_BrandyPetty 16 16JUL C_MelissaSmith 16
    17JUL C_AlyssaStevens 16 23JUL C_SandraBauer 16 25JUL C_JamesJackson 16 25JUL C_JamesJackson 16 29JUL C_TylerMccall 16
    30JUL C_NicholasWilliams 16 30JUL C_NicholasWilliams 17 14MAR C_MatthewMartinez 16 01AUG C_JacobOrtiz 16 05AUG
    C_CarolynWeber 16 06AUG C_TiffanySmith 16 09AUG C_JenniferPatrick 16 16AUG C_CarlVelazquez 16 19AUG C_BrandonMartinez 16
    19AUG C_BrandonMartinez 17 27JUN C_ChristinaGonzalez 16 31AUG C_BradleyValdez 16 31AUG C_JessicaTate 16 06SEP
    C_RichardMoore 16 06SEP C_SeanMacias 16 08SEP C_ZoeClark 16 11SEP C_AbigailJohnson 16 21SEP C_ElizabethByrd 16 20SEP
    C_ScottStone 16 20SEP C_ScottStone 16 22SEP C_MatthewLee 16 25SEP C_RobertBarry 16 27SEP C_JenniferHansen 16 27SEP
    C_DonnaHawkins 16 27SEP C_DonnaBrooks 16 30SEP C_KatelynSpencer 16 29SEP C_RaymondLutz 16 01OCT C_StevenKeller 16 05OCT
    C_DanaSmith 16 05OCT C_NathanBrown 16 04OCT C_MichaelScott 16 04OCT C_MrMichael 16 07OCT C_MarkBenitez 16 14OCT
    C_WilliamFord 16 28OCT C_AmandaCruz 16 14OCT C_PaulLandry 16 21OCT C_MrJoseph 16 25OCT C_CoryRodriguez 16 24OCT
    C_JacobSullivan 16 28OCT C_MrBrian 16 25OCT C_CoryRodriguez 16 28OCT C_AmandaCruz 17 17JAN C_RandallBarr 16 28OCT
    C_MrBrian 16 04NOV C_SharonHart 16 05NOV C_StephanieNolan 16 14NOV C_CassidySmith 16 16NOV C_MargaretRussell 16 15NOV
    C_PaulTaylor 16 16NOV C_SarahCarrillo 16 16NOV C_ValerieDean 16 21NOV C_JohnWhite 16 22NOV C_StaceyMueller 16 30NOV
    C_AshleyBlack 16 02DEC C_BrianMurphy 16 29DEC C_ThomasMorris 17 18JAN C_DavidMoore 17 15JAN C_TammySmith 17 15JAN
    C_TammySmith 17 25JAN C_MariaKing 17 27JAN C_MaryMartinez 17 26JAN C_DeniseThompson 17 30JAN C_MichaelRodriguez 17 07FEB
    C_AprilMartin 17 07FEB C_AnthonyWilliams 17 08FEB C_TraceyWilkins 17 11FEB C_JohnJohnson 17 10FEB C_LindseyRoss 17 11FEB
    C_JohnJohnson 17 14FEB C_TonyaJohnson 17 14FEB C_TonyaJohnson 17 22FEB C_LindaGarcia 17 22FEB C_LindaGarcia 17 22FEB
    C_ErnestKidd 17 21FEB C_SteveYu 17 22FEB C_SusanDelgado 17 24FEB C_JessicaHill 17 25FEB C_DavidBrooks 17 26FEB
    C_KevinNichols 17 04MAR C_SteveSchmidt 17 05MAR C_KeithHarper 17 07MAR C_StevenLindsey 17 11MAR C_MatthewParker 17 11MAR
    C_WhitneyPatterson 17 15MAR C_RandyHoffman 17 22MAR C_SarahAguilar 17 27MAR C_ThomasThompson 17 30MAR
    C_ChristopherFarmer 17 07APR C_GregoryWolf 17 08APR C_KristenBrewer 17 12APR C_CatherineWiggins 17 11APR
    C_HeatherHawkins 17 14APR C_AndrewPeterson 17 13APR C_TimothySmith 17 17APR C_ChristopherWilliams 17 19APR C_BrianMiller
    17 19APR C_BrianMiller 17 24APR C_JuliaBeck 17 29APR C_BarbaraPetersen 17 30APR C_WhitneyHorton 17 01MAY C_ThomasAustin
    17 08MAY C_JacquelineVelasquez 17 09MAY C_MelindaLowery 17 11MAY C_ThomasWells 17 10MAY C_AnneSmith 17 13MAY
    C_TammyVilla 17 14MAY C_TiffanyHurst 17 16MAY C_LoriChang 17 19MAY C_RebeccaGlover 17 20MAY C_GregorySmith 17 20MAY
    C_JoshuaMiddleton 17 24MAY C_DonaldKing 17 24MAY C_CherylLewis 17 27MAY C_BrandonGuzman 17 29MAY C_AlexandraBrown 17
    29MAY C_GinaSmith 17 01JUN C_JeffMiller 17 04JUN C_MaryHouston 17 16JUN C_KristinRhodes 17 09JUN C_KarenLewis 17 07JUN
    C_DouglasMartin 17 12JUN C_HeatherDuncan 17 11JUN C_MichaelClay 17 18JUN C_ChristopherFuentes 17 28JUN C_DouglasSalinas
    17 27JUN C_ChristinaGonzalez 17 03JUL C_JenniferJohnson 17 05JUL C_MichaelGarcia 17 06JUL C_AngelWhite 17 06JUL
    C_AngelWhite 17 06JUL C_KellySmith 17 07JUL C_SaraWillis 17 06JUL C_KellySmith 17 09JUL C_AaronCook 17 13JUL
    C_JessicaLee 17 15JUL C_ColleenLang 17 13JUL C_JoshuaCain 17 13JUL C_JessicaLee 17 16JUL C_GinaMerritt 17 16JUL
    C_MelissaSmith 17 20JUL C_FrankWilliams 17 16JUL C_CatherineDixon 17 22JUL C_CindyRamirez 17 30JUL C_AmberHopkins 17
    27JUL C_StevenLamb 17 05AUG C_DavidSmith 17 03AUG C_AmandaHood 17 07AUG C_AngelaAdkins 17 11AUG C_MichelleRocha 17 07AUG
    C_GinaCarter 17 14AUG C_MichaelWilliams 17 19AUG C_JenniferHall 17 25AUG C_MichaelTaylor 17 25AUG C_MichaelTaylor 17
    19AUG C_JenniferHall 17 25AUG C_AngelGriffith 17 30AUG C_SarahMiller
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* SD1.HAVE total obs=471                                                                                                 */
    /*                                                                                                                        */
    /* Obs    YEAR     DAY     HOTEL_GUEST                                                                                    */
    /*                                                                                                                        */
    /*   1     15     13JUL    R_ShannonWilcox                                                                                */
    /*   2     15     14JUL    R_JamesCobb                                                                                    */
    /*   3     15     07AUG    R_JasonAnderson                                                                                */
    /*   4     15     18AUG    R_MichelleSmith                                                                                */
    /*   5     15     02OCT    R_DanielleMendoza                                                                              */
    /*   6     15     19OCT    R_MonicaAllen                                                                                  */
    /*   7     15     23OCT    R_JosephFoster                                                                                 */
    /*   8     15     05DEC    R_AngelaGrant                                                                                  */
    /*   9     15     30DEC    R_TaylorLutz                                                                                   */
    /*  10     16     24MAR    R_TaylorShea                                                                                   */
    /*  11     16     14MAY    R_AngelChen                                                                                    */
    /*  12     16     21JUN    R_GregoryYoung                                                                                 */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                                       _         _
    / | __      ___ __  ___   ___  ___  _ __| |_    __| |_   _ _ __    __ _ _ __ ___  _   _ _ __  ___
    | | \ \ /\ / / `_ \/ __| / __|/ _ \| `__| __|  / _` | | | | `_ \  / _` | `__/ _ \| | | | `_ \/ __|
    | |  \ V  V /| |_) \__ \ \__ \ (_) | |  | |_  | (_| | |_| | |_) || (_| | | | (_) | |_| | |_) \__ \
    |_|   \_/\_/ | .__/|___/ |___/\___/|_|   \__|  \__,_|\__,_| .__/  \__, |_|  \___/ \__,_| .__/|___/
                 |_|                                          |_|     |___/                |_|
    */

    libname sd1 "d:/sd1";

    proc datasets lib=sd1 nolist nodetails;delete want; run;quit;

    proc sort data=sd1.have out=sd1.want nouniquekey;
     by year day hotel_guest;
    run;quit;

    /************************************************************************************************************************* */
    /*                                                                                                                         */
    /*  SD1.WANT total obs=155 02MAY2        QUICK WAY TO GET DUPLICATE GROUPS DOUBLE BOOKIGS                                  */
    /*                                                                                                                         */
    /*  YEAR     DAY     HOTEL_GUEST                                                                                           */
    /*                                                                                                                         */
    /*   15     05DEC    C_RobertLee                                                                                          */
    /*   15     05DEC    C_RobertLee                                                                                          */
    /*                                                                                                                        */
    /*   15     15OCT    C_LisaJones                                                                                          */
    /*   15     15OCT    C_LisaJones                                                                                          */
    /*                                                                                                                        */
    /*   15     19NOV    C_ChristopherMoore                                                                                   */
    /*   15     19NOV    C_ChristopherMoore                                                                                   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

     /*___                                   _
    |___ \  __      ___ __  ___   ___  __ _| |
      __) | \ \ /\ / / `_ \/ __| / __|/ _` | |
     / __/   \ V  V /| |_) \__ \ \__ \ (_| | |
    |_____|   \_/\_/ | .__/|___/ |___/\__, |_|
                     |_|                 |_|
    */

    proc datasets lib=sd1 nolist nodetails;delete sameyear difYear; run;quit;

    %utl_submit_wps64x('
    libname sd1 "d:/sd1";
    options validvarname=any;
    proc sql;
      create
         table sd1.havAll as
        select
          *
         ,case
            when (count(distinct(year))=2) then "DIFYEAR "
            when (count(year)          =2) then "SAMEYEAR"
            else "DELETE"
          end as status
        from
          sd1.have
        group
          by day, hotel_guest
        ;

      create
         table sd1.sameyear_wps as
        select
          *
        from
          sd1.havAll
        where
          status="SAMEYEAR"
     ;
      create
         table sd1.difyear_wps as
        select
          *
        from
          sd1.havAll
        where
          status="DIFYEAR"
     ;quit;

    ');

    proc print data=sd1.sameyear_wps width=min;
    run;quit;

    proc print data=sd1.difyear_wps width=min;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  SD1.HAVALL total obs=471                                                                                              */
    /*                                                                                                                        */
    /*   YEAR     DAY     HOTEL_GUEST             STATUS                                                                      */
    /*                                                                                                                        */
    /*    17     01APR    R_JesseMorales         DELETE                                                                       */
    /*    15     01AUG    C_DianeCarpenter       DELETE                                                                       */
    /*    16     01AUG    C_JacobOrtiz           DELETE                                                                       */
    /*    16     01DEC    R_AshleyHester         DELETE                                                                       */
    /*    15     01JUL    C_MrRobert             DIFYEAR                                                                      */
    /*    16     01JUL    C_MrRobert             DIFYEAR                                                                      */
    /*    16     01JUL    C_TroyIngram           DELETE                                                                       */
    /*    17     01JUN    C_JeffMiller           DELETE                                                                       */
    /*    17     01MAY    C_ThomasAustin         DELETE                                                                       */
    /*    16     01OCT    C_StevenKeller         DELETE                                                                       */
    /*    15     01OCT    R_AmandaBond           DELETE                                                                       */
    /*    15     01SEP    C_RyanStewart          DELETE                                                                       */
    /*    16     01SEP    R_NicoleHall           DELETE                                                                       */
    /*    16     02APR    C_RobertBrown          DELETE                                                                       */
    /*    16     02AUG    R_VincentDunn          DELETE                                                                       */
    /*    16     02DEC    C_BrianMurphy          DELETE                                                                       */
    /*    16     02JAN    C_MrsKaren             DELETE                                                                       */
    /*    16     02JAN    C_RobertMedina         DELETE                                                                       */
    /*    17     02JAN    R_MatthewLee           SAMEYEAR                                                                     */
    /*    17     02JAN    R_MatthewLee           SAMEYEAR                                                                     */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  SD1.SAMEYEAR_WPS total obs=84                                                                                         */
    /*                                                                                                                        */
    /*   YEAR     DAY     HOTEL_GUEST            STATUS                                                                       */
    /*                                                                                                                        */
    /*    17     02JAN    R_MatthewLee          SAMEYEAR                                                                      */
    /*    17     02JAN    R_MatthewLee          SAMEYEAR                                                                      */
    /*    16     03DEC    R_JenniferCarlson     SAMEYEAR                                                                      */
    /*    16     03DEC    R_JenniferCarlson     SAMEYEAR                                                                      */
    /*    15     05DEC    C_RobertLee           SAMEYEAR                                                                      */
    /*    15     05DEC    C_RobertLee           SAMEYEAR                                                                      */
    /*    16     06APR    C_NicoleKlein         SAMEYEAR                                                                      */
    /*    16     06APR    C_NicoleKlein         SAMEYEAR                                                                      */
    /*    17     06JUL    C_AngelWhite          SAMEYEAR                                                                      */
    /*    17     06JUL    C_AngelWhite          SAMEYEAR                                                                      */
    /*    17     06JUL    C_KellySmith          SAMEYEAR                                                                      */
    /*    17     06JUL    C_KellySmith          SAMEYEAR                                                                      */
    /*    16     07MAR    C_LaurenDavis         SAMEYEAR                                                                      */
    /*    16     07MAR    C_LaurenDavis         SAMEYEAR                                                                      */
    /*    16     09JUN    C_ChristopherJones    SAMEYEAR                                                                      */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  SD1.DIFYEAR_WPS total obs=71                                                                                          */
    /*                                                                                                                        */
    /*   YEAR     DAY     HOTEL_GUEST              STATUS                                                                     */
    /*                                                                                                                        */
    /*    15     01JUL    C_MrRobert             DIFYEAR                                                                      */
    /*    16     01JUL    C_MrRobert             DIFYEAR                                                                      */
    /*    17     03JUL    C_JenniferJohnson      DIFYEAR                                                                      */
    /*    16     03JUL    C_JenniferJohnson      DIFYEAR                                                                      */
    /*    16     04OCT    C_MichaelScott         DIFYEAR                                                                      */
    /*    15     04OCT    C_MichaelScott         DIFYEAR                                                                      */
    /*    16     04OCT    C_MrMichael            DIFYEAR                                                                      */
    /*    15     04OCT    C_MrMichael            DIFYEAR                                                                      */
    /*    17     05AUG    C_DavidSmith           DIFYEAR                                                                      */
    /*    15     05AUG    C_DavidSmith           DIFYEAR                                                                      */
    /*    16     05JUL    C_MichaelGarcia        DIFYEAR                                                                      */
    /*    17     05JUL    C_MichaelGarcia        DIFYEAR                                                                      */
    /*    16     05OCT    C_DanaSmith            DIFYEAR                                                                      */
    /*    15     05OCT    C_DanaSmith            DIFYEAR                                                                      */
    /*    16     06AUG    C_TiffanySmith         DIFYEAR                                                                      */
    /*    15     06AUG    C_TiffanySmith         DIFYEAR                                                                      */
    /*    15     06OCT    R_MarkBrown            DIFYEAR                                                                      */
    /*    16     06OCT    R_MarkBrown            DIFYEAR                                                                      */
    /*    17     07MAR    R_MichaelFerguson      DIFYEAR                                                                      */
    /*                                                                                                                        */
    /**************************************************************************************************************************/


    /*____                                         _
    |___ /  __      ___ __  ___   _ __   ___  __ _| |
      |_ \  \ \ /\ / / `_ \/ __| | `__| / __|/ _` | |
     ___) |  \ V  V /| |_) \__ \ | |    \__ \ (_| | |
    |____/    \_/\_/ | .__/|___/ |_|    |___/\__, |_|
                     |_|                        |_|
    */

    proc datasets lib=sd1 nolist nodetails;delete sameyear difYear; run;quit;

    %utl_submit_wps64x('
    libname sd1 "d:/sd1";
    proc r;
    export data=sd1.have r=have;
    submit;
    library(sqldf);
    sameyear<-sqldf("
      select
         l.year
        ,l.day
        ,l.hotel_guest
        ,r.sameyear
      from
         have as l inner join
            ( select
                *
               ,count(*) as sameyear
              from
                have
              group
                by day, hotel_guest, year
            ) as r
      on
             l.year        = r.year
         and l.day         = r.day
         and l.hotel_guest = r.hotel_guest
         and sameyear > 1
      order
         by l.day, l.hotel_guest, l.year
    ");
    sameyear;
    difyear <-sqldf("
      select
         l.year
        ,l.day
        ,l.hotel_guest
        ,r.difyear
      from
         have as l inner join
            ( select
                *
               ,count(distinct year) as difyear
              from
                have
              group
                by day, hotel_guest
            ) as r
      on
             l.day         = r.day
         and l.hotel_guest = r.hotel_guest
         and  difyear > 1
      order
         by l.day, l.hotel_guest, l.year
    ");
    difyear;
    endsubmit;
    import data=sd1.sameyear r=sameyear;
    import data=sd1.difyear  r=difyear;
    run;quit;
    ');

    proc print data=sd1.sameyear;
    run;quit;

    proc print data=sd1.difyear;
    run;quit;

     /**************************************************************************************************************************/
     /*                                                                                                                        */
     /*  SD1.SAMEYEAR total obs=86              SD1.DIFYEAR total obs=71                                                       */
     /*                                                                                                                        */
     /*   YEAR     DAY     HOTEL_GUEST          YEAR     DAY     HOTEL_GUEST              DIFYEA                               */
     /*                                                                                                                        */
     /*    17     02JAN    R_MatthewLee          15     01JUL    C_MrRobert                  2                                 */
     /*    17     02JAN    R_MatthewLee          16     01JUL    C_MrRobert                  2                                 */
     /*    16     03DEC    R_JenniferCarlson     16     03JUL    C_JenniferJohnson           2                                 */
     /*    16     03DEC    R_JenniferCarlson     17     03JUL    C_JenniferJohnson           2                                 */
     /*    15     05DEC    C_RobertLee           15     04OCT    C_MichaelScott              2                                 */
     /*    15     05DEC    C_RobertLee           16     04OCT    C_MichaelScott              2                                 */
     /*    16     06APR    C_NicoleKlein         15     04OCT    C_MrMichael                 2                                 */
     /*    16     06APR    C_NicoleKlein         16     04OCT    C_MrMichael                 2                                 */
     /*    17     06JUL    C_AngelWhite          15     05AUG    C_DavidSmith                2                                 */
     /*    17     06JUL    C_AngelWhite          17     05AUG    C_DavidSmith                2                                 */
     /*    17     06JUL    C_KellySmith          16     05JUL    C_MichaelGarcia             2                                 */
     /*    17     06JUL    C_KellySmith          17     05JUL    C_MichaelGarcia             2                                 */
     /*    16     07MAR    C_LaurenDavis         15     05OCT    C_DanaSmith                 2                                 */
     /*    16     07MAR    C_LaurenDavis         16     05OCT    C_DanaSmith                 2                                 */
     /*                                                                                                                        */
     /**************************************************************************************************************************/

    /*  _                                      _   _                             _
    | || |   __      ___ __  ___   _ __  _   _| |_| |__   ___  _ __    ___  __ _| |
    | || |_  \ \ /\ / / `_ \/ __| | `_ \| | | | __| `_ \ / _ \| `_ \  / __|/ _` | |
    |__   _|  \ V  V /| |_) \__ \ | |_) | |_| | |_| | | | (_) | | | | \__ \ (_| | |
       |_|     \_/\_/ | .__/|___/ | .__/ \__, |\__|_| |_|\___/|_| |_| |___/\__, |_|
                      |_|         |_|    |___/                                |_|
    */



    %utl_submit_wps64x("
    options validvarname=any lrecl=32756;
    libname sd1 'd:/sd1';
    proc python;
    export data=sd1.have python=have;
    submit;
    print(have);
    from os import path;
    import pandas as pd;
    import numpy as np;
    from pandasql import sqldf;
    mysql = lambda q: sqldf(q, globals());
    from pandasql import PandaSQL;
    pdsql = PandaSQL(persist=True);
    sqlite3conn = next(pdsql.conn.gen).connection.connection;
    sqlite3conn.enable_load_extension(True);
    sqlite3conn.load_extension('c:/temp/libsqlitefunctions.dll');
    mysql = lambda q: sqldf(q, globals());
    sameyear = pdsql('''
      select
         l.year
        ,l.day
        ,l.hotel_guest
        ,r.sameyear
      from
         have as l inner join
            ( select
                *
               ,count(*) as sameyear
              from
                have
              group
                by day, hotel_guest, year
            ) as r
      on
             l.year        = r.year
         and l.day         = r.day
         and l.hotel_guest = r.hotel_guest
         and sameyear > 1
      order
         by l.day, l.hotel_guest, l.year
    ''');
    print(sameyear);
    difyear = pdsql('''
      select
         l.year
        ,l.day
        ,l.hotel_guest
        ,r.difyear
      from
         have as l inner join
            ( select
                *
               ,count(distinct year) as difyear
              from
                have
              group
                by day, hotel_guest
            ) as r
      on
             l.day         = r.day
         and l.hotel_guest = r.hotel_guest
         and  difyear > 1
      order
         by l.day, l.hotel_guest, l.year
    ''');
    print(difyear);
    endsubmit;
    run;quit;
    ");

    proc print data=sd1.want;
    run;quit;


    %utl_submit_wps64x('
    libname sd1 "d:/sd1";
    proc r;
    export data=sd1.have r=have;
    submit;
    library(sqldf);
    idDups<-sqldf("
        select
            year
           ,day
           ,hotel_guest
           ,count(distinct year) as difyear
        from
           have
        group
           by day, hotel_guest
        having
           count(distinct year) > 1
    ");
    idDups;
    endsubmit;
    ');

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*   _                   _                                                                                                */
    /*  (_)_ __  _ __  _   _| |_                                                                                              */
    /*  | | `_ \| `_ \| | | | __|                                                                                             */
    /*  | | | | | |_) | |_| | |_                                                                                              */
    /*  |_|_| |_| .__/ \__,_|\__|                                                                                             */
    /*          |_|                                                                                                           */
    /*                                                                                                                        */
    /*  The WPS System                                                                                                        */
    /*                                                                                                                        */
    /*  The PYTHON Procedure                                                                                                  */
    /*                                                                                                                        */
    /*      YEAR    DAY   HOTEL_GUEST                                                                                         */
    /*  0     15  13JUL  R_ShannonWilcox                                                                                      */
    /*  1     15  14JUL  R_JamesCobb                                                                                          */
    /*  2     15  07AUG  R_JasonAnderson                                                                                      */
    /*  3     15  18AUG  R_MichelleSmith                                                                                      */
    /*  4     15  02OCT  R_DanielleMendoza                                                                                    */
    /*  ..   ...    ...                                                                                                       */
    /*  466   17  25AUG  C_MichaelTaylor                                                                                      */
    /*  467   17  25AUG  C_MichaelTaylor                                                                                      */
    /*  468   17  19AUG  C_JenniferHall                                                                                       */
    /*  469   17  25AUG  C_AngelGriffith                                                                                      */
    /*  470   17  30AUG  C_SarahMiller                                                                                        */
    /*                                                                                                                        */
    /*  ___  __ _ _ __ ___   ___ _   _  ___  __ _ _ __                                                                        */
    /* / __|/ _` | `_ ` _ \ / _ \ | | |/ _ \/ _` | `__|                                                                       */
    /* \__ \ (_| | | | | | |  __/ |_| |  __/ (_| | |                                                                          */
    /* |___/\__,_|_| |_| |_|\___|\__, |\___|\__,_|_|                                                                          */
    /*                           |___/                                                                                        */
    /*                                                                                                                        */
    /*     YEAR    DAY   HOTEL_GUEST                                                                                          */
    /*  0    17  02JAN  R_MatthewLee                                                                                          */
    /*  1    17  02JAN  R_MatthewLee                                                                                          */
    /*  2    16  03DEC  R_JenniferCarlson                                                                                     */
    /*  3    16  03DEC  R_JenniferCarlson                                                                                     */
    /*  4    15  05DEC  C_RobertLee                                                                                           */
    /*  ..  ...    ...                                                                                                        */
    /*  81   16  30JUL  C_NicholasWilliams                                                                                    */
    /*  82   17  30JUL  R_DouglasBrown                                                                                        */
    /*  83   17  30JUL  R_DouglasBrown                                                                                        */
    /*  84   16  30JUN  C_StevenArmstrong                                                                                     */
    /*  85   16  30JUN  C_StevenArmstrong                                                                                     */
    /*      _ _  __                                                                                                           */
    /*   __| (_)/ _|_   _  ___  __ _ _ __                                                                                     */
    /*  / _` | | |_| | | |/ _ \/ _` | `__|                                                                                    */
    /* | (_| | |  _| |_| |  __/ (_| | |                                                                                       */
    /*  \__,_|_|_|  \__, |\___|\__,_|_|                                                                                       */
    /*              |___/                                                                                                     */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*     YEAR    DAY   HOTEL_GUEST                                                                                          */
    /*  0    15  01JUL  C_MrRobert                                                                                            */
    /*  1    16  01JUL  C_MrRobert                                                                                            */
    /*  2    16  03JUL  C_JenniferJohnson                                                                                     */
    /*  3    17  03JUL  C_JenniferJohnson                                                                                     */
    /*  4    15  04OCT  C_MichaelScott                                                                                        */
    /*  ..  ...    ...                                                                                                        */
    /*  66   17  29MAY  C_AlexandraBrown                                                                                      */
    /*  67   16  29MAY  C_GinaSmith                                                                                           */
    /*  68   17  29MAY  C_GinaSmith                                                                                           */
    /*  69   16  30JAN  C_MichaelRodriguez                                                                                    */
    /*  70   17  30JAN  C_MichaelRodriguez                                                                                    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
