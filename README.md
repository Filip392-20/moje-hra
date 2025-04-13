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
    int zlato = 0;
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

    // Souboj dokud nekdo nezemre
    while (hrac.classy.zivoty > 0 && goblin.zivoty > 0) {
        cout << "\nTvoje zivoty: " << hrac.classy.zivoty;
        cout << "\nZivoty goblina: " << goblin.zivoty << endl;

        cout << "\nZmackni ENTER pro utok...";
        cin.ignore();
        cin.get();

        // Hrac utoci
        goblin.zivoty -= hrac.classy.utok;
        cout << "Zasahl jsi goblina za " << hrac.classy.utok << " poskozeni.\n";

        if (goblin.zivoty <= 0) {
            cout << goblin.jmeno << " padl!\n";
            break;
        }

        // Goblin utoci
        hrac.classy.zivoty -= goblin.utok;
        cout << "Goblin te zasahl za " << goblin.utok << " poskozeni.\n";

        if (hrac.classy.zivoty <= 0) {
            cout << "Byl jsi porazen...\n";
            break;
        }
    }

    // Konec boje
    if (hrac.classy.zivoty > 0) {
        cout << "\nVyhral jsi prvni souboj!\n";
    }

    cout << "\nDiky za hrani!\n";

    return 0;
}
