#include <iostream>
#include <string>
using namespace std;

// Struktura pro classu postavy
struct PostavaClass {
    string jmeno;
    int maxZivoty;
    int zivoty;
    int utok;
};

// Hracova data
struct Hrac {
    PostavaClass classy;
    int zlato = 10; // zaèínáme se zlatem
};

// Monstrum
struct Prisera {
    string jmeno;
    int zivoty;
    int utok;
};

// Zobrazeni informace o classe
void ukazClassu(PostavaClass c) {
    cout << "\nZvolena classa: " << c.jmeno << endl;
    cout << "Zivoty: " << c.zivoty << "/" << c.maxZivoty << endl;
    cout << "Utok: " << c.utok << endl;
}

// Funkce pro vesnici
void vesnice(Hrac& hrac) {
    cout << "\nDorazil jsi do vesnice.\n";
    cout << "Zde si muzes odpocinout nebo se vylepsit.\n";

    bool veVesnici = true;

    while (veVesnici) {
        cout << "\nMas " << hrac.zlato << " zlata.\n";
        cout << "1) Doplnit zivoty (5 zlata)\n";
        cout << "2) Zvysit max zivoty o 1 (10 zlata)\n";
        cout << "3) Odejit z vesnice\n";
        cout << "Zadej volbu: ";

        int volba;
        cin >> volba;

        if (volba == 1) {
            if (hrac.zlato >= 5) {
                hrac.zlato -= 5;
                hrac.classy.zivoty = hrac.classy.maxZivoty;
                cout << "Doplnil sis vsechny zivoty.\n";
            } else {
                cout << "Nemas dost zlata!\n";
            }
        } else if (volba == 2) {
            if (hrac.zlato >= 10) {
                hrac.zlato -= 10;
                hrac.classy.maxZivoty += 1;
                hrac.classy.zivoty = hrac.classy.maxZivoty;
                cout << "Zvysil sis maximalni pocet zivotu o 1.\n";
            } else {
                cout << "Nemas dost zlata!\n";
            }
        } else if (volba == 3) {
            veVesnici = false;
            cout << "Opoustis vesnici.\n";
        } else {
            cout << "Neplatna volba.\n";
        }
    }
}

int main() {
    Hrac hrac;
    string volba;

    // Nabidka classy
    while (true) {
        cout << "Vyber si postavu:\n";
        cout << "1. Paladin\n";
        cout << "2. Mag\n";
        cout << "3. Lovec\n";
        cout << "4. Warlock\n";
        cout << "Zadej cislo classy: ";
        cin >> volba;

        if (volba == "1") {
            PostavaClass paladin = {"Paladin", 6, 6, 3};
            ukazClassu(paladin);
            cout << "Chces tuto postavu? (a/n): ";
            cin >> volba;
            if (volba == "a") {
                hrac.classy = paladin;
                break;
            }
        } else if (volba == "2") {
            PostavaClass mag = {"Mag", 4, 4, 5};
            ukazClassu(mag);
            cout << "Chces tuto postavu? (a/n): ";
            cin >> volba;
            if (volba == "a") {
                hrac.classy = mag;
                break;
            }
        } else if (volba == "3") {
            PostavaClass lovec = {"Lovec", 5, 5, 4};
            ukazClassu(lovec);
            cout << "Chces tuto postavu? (a/n): ";
            cin >> volba;
            if (volba == "a") {
                hrac.classy = lovec;
                break;
            }
        } else if (volba == "4") {
            PostavaClass warlock = {"Warlock", 5, 5, 3};
            ukazClassu(warlock);
            cout << "Chces tuto postavu? (a/n): ";
            cin >> volba;
            if (volba == "a") {
                hrac.classy = warlock;
                break;
            }
        } else {
            cout << "Spatna volba. Zkus to znovu.\n";
        }
    }

    // Prvni souboj
    Prisera goblin;
    goblin.jmeno = "Goblin";
    goblin.zivoty = 4;
    goblin.utok = 2;

    cout << "\nNarazil jsi na prisera: " << goblin.jmeno << "!\n";
    cout << "Zacina boj!\n";

    cin.ignore(); // opravuje problém se stiskem enteru

    while (hrac.classy.zivoty > 0 && goblin.zivoty > 0) {
        cout << "\nTvoje zivoty: " << hrac.classy.zivoty;
        cout << "\nZivoty goblina: " << goblin.zivoty << endl;

        cout << "\nZmackni ENTER pro utok...";
        cin.get();

        goblin.zivoty -= hrac.classy.utok;
        cout << "Zasahl jsi goblina za " << hrac.classy.utok << " poskozeni.\n";

        if (goblin.zivoty <= 0) {
            cout << goblin.jmeno << " padl!\n";
            break;
        }

        hrac.classy.zivoty -= goblin.utok;
        cout << "Goblin te zasahl za " << goblin.utok << " poskozeni.\n";

        if (hrac.classy.zivoty <= 0) {
            cout << "Byl jsi porazen...\n";
            return 0;
        }
    }

    if (hrac.classy.zivoty > 0) {
        cout << "\nVyhral jsi prvni souboj!\n";
    }

    // Druhy souboj
    if (hrac.classy.zivoty > 0) {
        cout << "\nPo prvnim souboji pokracujes dal...\n";

        Prisera kostlivec1 = {"Kostlivec A", 3, 2};
        Prisera kostlivec2 = {"Kostlivec B", 3, 2};

        cout << "\nZ utrob se vynorili 2 kostlivci!\n";
        cout << "Priprav se na boj proti obema zaraz!\n";

        while (hrac.classy.zivoty > 0 && (kostlivec1.zivoty > 0 || kostlivec2.zivoty > 0)) {
            cout << "\nTvoje zivoty: " << hrac.classy.zivoty << endl;
            cout << "Kostlivec A: " << kostlivec1.zivoty << "  |  Kostlivec B: " << kostlivec2.zivoty << endl;

            cout << "\nZvol, na koho chces utocit (a / b): ";
            string cil;
            cin >> cil;

            if (cil == "a" && kostlivec1.zivoty > 0) {
                kostlivec1.zivoty -= hrac.classy.utok;
                cout << "Zasahl jsi Kostlivce A za " << hrac.classy.utok << " poskozeni.\n";
            } else if (cil == "b" && kostlivec2.zivoty > 0) {
                kostlivec2.zivoty -= hrac.classy.utok;
                cout << "Zasahl jsi Kostlivce B za " << hrac.classy.utok << " poskozeni.\n";
            } else {
                cout << "Spatny cil nebo uz mrtvy.\n";
            }

            if (kostlivec1.zivoty > 0) {
                hrac.classy.zivoty -= kostlivec1.utok;
                cout << "Kostlivec A te zasahl za " << kostlivec1.utok << " poskozeni.\n";
            }

            if (kostlivec2.zivoty > 0) {
                hrac.classy.zivoty -= kostlivec2.utok;
                cout << "Kostlivec B te zasahl za " << kostlivec2.utok << " poskozeni.\n";
            }

            if (hrac.classy.zivoty <= 0) {
                cout << "Byl jsi porazen...\n";
                return 0;
            }
        }

        cout << "\nZvitezil jsi nad obema kostlivci!\n";

        // >>> Tady spravne zavolame vesnici
        vesnice(hrac);
       // Pokracovani po vesnici - cesta do temneho lesa
    cout << "\nPo odpocinku ve vesnici se vydavas do temneho lesa...\n";
    cout << "Les je plny nebezpeci, ale take pokladu.\n";

    // Tri nepratele najednou
    Prisera elf = {"Temny Elf", 4, 2};
    Prisera pavouk = {"Zmutovany Pavouk", 5, 3};
    Prisera stin = {"Stin", 6, 2};

    cout << "\nNarazil jsi na tri nepratele!\n";
    cout << elf.jmeno << ", " << pavouk.jmeno << " a " << stin.jmeno << "!\n";

    // Souboj
    while (hrac.classy.zivoty > 0 && (elf.zivoty > 0 || pavouk.zivoty > 0 || stin.zivoty > 0)) {
        cout << "\nTvoje zivoty: " << hrac.classy.zivoty << endl;
        cout << elf.jmeno << ": " << elf.zivoty << " | ";
        cout << pavouk.jmeno << ": " << pavouk.zivoty << " | ";
        cout << stin.jmeno << ": " << stin.zivoty << endl;

        cout << "\nZvol, na koho chces utocit (e = elf, p = pavouk, s = stin): ";
        string cil;
        cin >> cil;

        if (cil == "e" && elf.zivoty > 0) {
            elf.zivoty -= hrac.classy.utok;
            cout << "Zasahl jsi " << elf.jmeno << " za " << hrac.classy.utok << " poskozeni.\n";
        } else if (cil == "p" && pavouk.zivoty > 0) {
            pavouk.zivoty -= hrac.classy.utok;
            cout << "Zasahl jsi " << pavouk.jmeno << " za " << hrac.classy.utok << " poskozeni.\n";
        } else if (cil == "s" && stin.zivoty > 0) {
            stin.zivoty -= hrac.classy.utok;
            cout << "Zasahl jsi " << stin.jmeno << " za " << hrac.classy.utok << " poskozeni.\n";
        } else {
            cout << "Spatny cil nebo uz je porazen.\n";
        }

        // Utok nepratel
        if (elf.zivoty > 0) {
            hrac.classy.zivoty -= elf.utok;
            cout << elf.jmeno << " te zasahl za " << elf.utok << " poskozeni.\n";
        }
        if (pavouk.zivoty > 0) {
            hrac.classy.zivoty -= pavouk.utok;
            cout << pavouk.jmeno << " te kousl za " << pavouk.utok << " poskozeni.\n";
        }
        if (stin.zivoty > 0) {
            hrac.classy.zivoty -= stin.utok;
            cout << stin.jmeno << " ti ubral " << stin.utok << " stinove poskozeni.\n";
        }

        if (hrac.classy.zivoty <= 0) {
            cout << "Byl jsi porazen temnymi silami lesa...\n";
            return 0;
        }
    }

    cout << "\nZvitezil jsi nad neprateli z temneho lesa!\n";
    hrac.zlato += 15;
    cout << "Ziskal jsi 15 zlata. Mas ted " << hrac.zlato << " zlata.\n";
    cout << "Pokracovani priste...\n";

   }

    cout << "\nDiky za hrani!\n";
    return 0;
}
