# seprog_16bit
16bit chip adapter for the WG Electronics Seprog programmer

## Info in english:
This repo describes a 16-bit chip adapter for the eprom programmer "Seprog" from the polish manufacturer WG Electronics. The rest will be in polish, because I don't belive that anyone outside of Poland will be interested in this information.

To repozytorium zawiera schemat i płytkę zaprojektowaną w oprogramowaniu Kicad do adaptera do 16-bitowych układów EPROM (tych kasowalnych UV) do programatora Seprog firmy WG Electronics. Schemat opracowałem przez analizę działania mojego programatora z firmware w wersji 1.49 (bardzo możliwe, że niższe wersje oprogramowania nie wspierają tych układów, 1.00 nie wspiera - sprawdzono).

Obsługiwane układy (natywnie, przez programator i oryginalne oprogramowanie), podstawka DIL40:
- 27C1024
- 27C2048
- 27C4096

Mój adapter umożliwia ponadto programowanie, podstawka DIL42:
- 27C160
- 27C322
- 27C400
- 27C800

przez ręczne przełączanie banków pamięci (pomysł z https://github.com/mafe72/27c160-tl866-adapter) używając w oprogramowaniu trybu 27C4096)

## Schemat adaptera:
![Schemat](/serprog_16bit_multi_adapter.svg)

## Problemy:
- Używając algorytmu INTELIgent programator zasila układ programowany (więc również nasz adapter) napięciem 6,25V (zgodnie z dokumentacją np. AM27C160), co już jest poza specyfikacją układów z serii 74HC. U mnie nawet na HCT działało dobrze i po wielu zapisach układy nie uległy uszkodzeniu, ale trzeba to mieć na uwadze.
- Aplikacja wSeprog napisana przez użytkownika jurex portalu elektroda.pl (https://www.elektroda.pl/rtvforum/topic857189.html) niestety niezupełnie poprawnie obsługuje układy 16 bitowe (konieczna jest zamiana sygnałów Q4 i Q6, tak robi oryginalne oprogramowanie pod DOSa, więc zakładam, że oryginalny adapter też tak miał)
- Wzór płytki nie został póki co sprawdzony w praktyce (mam wykonany prototyp z bankowaniem dla większych układów, ale nie przemyślałem aspektu dźwigienki podstawki ZIF programatora i potrzebne są długie goldpiny, adapter bardzo niestabilnie "siedzi").
- Programowanie jest bardzo powolne - ok. 15 minut na jeden bank "27C4096" i to jest czas dla najszybszego algorytmu INTELIgent


## Jeszcze kilka porad dla startujących z tym programatorem:
- Oryginalna aplikacja pod dosa chodzi bardzo dobrze z emulatorem DOSbox (https://www.dosbox.com/), trzeba tylko przekierować port COM emulatora do rzeczywistego portu komputera (może być adapter na USB, programator używa tylko linii RXD i TXD)
- Przypadki związane z losowymi błędami odczytu i zapisu mogą być spowodowane kiepskim zasilaniem. Powinien wystarczyć zasilacz niestabilizowany, oryginalnie chyba był 9V 500mA. Programator ma własny stabilizator 5V i przetwornicę impulsową (nie zapominajmy, że on obsługuje też bardzo stare EPROMy 21V!)

## Render 3D płytki
dla ciekawych

![Płytka3D](/serprog_16bit_multi_adapter_3d.jpg)
