# Lab-DL
Introduktion

Projektet siktar på att skapa en AI som kunde lära sig att spela det klassiska arkadspelet Space Invaders. Det har varit en riktigt spännande resa! Jag använde en metod som heter Deep Q-Learning, som är en typ av förstärkningsinlärning (Reinforcement Learning). I grund och botten byggde jag en "hjärna" (ett neuralt nätverk) som lär sig genom försök och misstag, precis som vi gör!

Målet

Mitt mål var att träna denna AI att få en hög poäng i Space Invaders utan att jag talade om för den exakt vad den skulle göra. Den var tvungen att lista ut de bästa strategierna helt själv.

Hur det fungerar: 

Miljö: Spelet Space Invaders är miljön.
Agent: Min AI är agenten
Tillstånd: Den aktuella situationen i spelet (var utomjordingarna är, var rymdskeppet är) är tillståndet.
Handling: Agenten kan vidta åtgärder, som att flytta åt vänster, höger eller skjuta.
Belöning: Agenten får en belöning för att göra bra saker, som att skjuta en utomjording. Den får en högre belöning för att klara en nivå.
Agentens mål är att lära sig vilka åtgärder den ska vidta i varje tillstånd för att få flest belöningar över tid.

"Hjärnan": Deep Q-Network (DQN)

AI:ns hjärna är ett Deep Q-Network. Här är en förenklad uppdelning:

Neuralt Nätverk: Det är som en förenklad version av vår egen hjärna, med sammankopplade noder. Den tar speltillståndet som input.
Convolutional Layers (faltningslager): Dessa lager är riktigt bra på att bearbeta bilder. De hjälper AI:n att förstå var utomjordingarna och rymdskeppet befinner sig utifrån spelbilden. Vi har tre stycken av dessa.
Den första har 32 filter och en storlek på 8x8 och en stride på 4x4.
Den andra har 64 filter och en storlek på 4x4 och en stride på 2x2.
Den sista har 64 filter och en storlek på 3x3 och en stride på 1x1.
Dense Layers (tätt sammankopplade lager): Efter att ha bearbetat bilden hjälper dessa lager AI:n att bestämma den bästa åtgärden att vidta. Vi har två stycken av dessa.
Den första har 512 neuroner och använder ReLU-aktiveringsfunktionen.
Den andra har samma antal utgångar som antalet möjliga åtgärder agenten kan vidta.

Q-värden: Nätverket matar ut ett "Q-värde" för varje möjlig åtgärd. Ju högre Q-värde, desto bättre tycker AI:n att den åtgärden är i det aktuella tillståndet.

Inlärning: AI:n lär sig genom att justera kopplingarna i det neurala nätverket baserat på de belöningar den får. Den använder en teknik som kallas "Huber loss" för att räkna ut hur den ska förbättra sina förutsägelser.
Träningsprocessen

Att träna AI:n involverade dessa steg:

Installation:

Jag använde biblioteket gymnasium för att simulera Space Invaders-spelet.
Jag använde också tensorflow för att bygga och träna det neurala nätverket.
Jag förbehandlade spelbilderna (gjorde dem i gråskala, skalade ner dem och staplade några bilder tillsammans så att AI:n kunde se rörelse).

Utforskning kontra Utnyttjande:

I början vidtar AI:n mestadels slumpmässiga åtgärder (utforskning) för att lära sig om spelet.
Allt eftersom den lär sig börjar den välja åtgärder baserat på sina Q-värden (utnyttjande), men den utforskar fortfarande lite för att se till att den inte missar bättre strategier.
Denna balans styrs av ett värde som kallas "epsilon", som börjar högt och minskar med tiden.

Återspelningsminne (Replay Memory):

AI:n lagrar sina erfarenheter (tillstånd, åtgärd, belöning, nästa tillstånd) i ett "återspelningsminne".
Den tar sedan slumpmässiga samplingar från detta minne för att lära sig. Detta hjälper den att lära sig från ett bredare spektrum av erfarenheter och bryter korrelationer mellan påföljande steg.

Målnätverk (Target Network):

Jag använde ett andra neuralt nätverk som kallas "målnätverket".
Detta nätverk uppdateras mer sällan och hjälper till att stabilisera inlärningsprocessen.

Träningsslinga:

AI:n spelade många episoder av spelet.
I varje episod vidtog den åtgärder, fick belöningar, lagrade erfarenheter och lärde sig från sitt minne.
Jag använde en optimerare som heter "Adam" med en inlärningshastighet på 0.00025 för att justera det neurala nätverkets vikter.

Koden i korthet

Environment Wrappers: AtariPreprocessing- och FrameStack-omslag från gymnasium gjorde spelet lättare för AI:n att förstå.
ReplayMemory-klass: Denna klass lagrade och samplade AI:ns erfarenheter effektivt.
choose_action-funktion: Denna funktion implementerade epsilon-greedy-strategin för att balansera utforskning och utnyttjande.
Träningsslinga: Det är här den huvudsakliga handlingen ägde rum, där AI:n spelade, lärde sig och förbättrades.
Resultat

Efter att ha tränat i 10000 episoder blev AI:n ganska bra på Space Invaders! Den lärde sig att skjuta utomjordingarna, undvika deras attacker och lärde sig till och med några avancerade strategier. Det var riktigt coolt att se den lära sig och bli bättre med tiden.

Utmaningar

Beräkningskostnad: Träningen tog lång tid eftersom AI:n var tvungen att spela många spel.
Hyperparameterjustering: Att hitta rätt inställningar (som inlärningshastighet, epsilon-förfall, etc.) var knepigt och involverade en del experimenterande.

Slutsats

Detta projekt var ett fantastiskt sätt att lära sig om förstärkningsinlärning och Deep Q-Networks. Det var utmanande men otroligt givande att se min AI lära sig att spela Space Invaders. Jag är verkligen exalterad över att utforska mer komplexa AI-tekniker i framtiden!

Framtida förbättringar

Experimentera med olika arkitekturer: Jag skulle kunna prova olika typer av neurala nätverk för att se om de presterar bättre.
Mer avancerade tekniker: Jag skulle kunna utforska tekniker som Double DQN eller Dueling DQN för att förbättra stabilitet och prestanda.
Träna på andra spel: Jag skulle kunna försöka träna AI:n att spela andra Atari-spel.
