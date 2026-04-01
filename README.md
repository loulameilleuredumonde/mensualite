#include <iostream>
#include <cmath>
#include <cstdio>
using namespace std;

#define COLS 4


class Emprunt {
    private:
        double capital;
        double tauxAnnuel;
        int nbMois;
        double tauxMensuel;
        double mensualite;

    public:
        Emprunt(double cap, int duree, double taux) {
            capital = cap;
            nbMois = duree * 12;
            tauxAnnuel = taux;
            tauxMensuel = (tauxAnnuel / 100) / 12;
            mensualite = 0;
        }

        double calculerMensualite() {
            double calcul1 = capital * tauxMensuel;
            double calcul2 = 1;

            for(int i = 0; i < nbMois; i++) {
                calcul2 *= (1 + tauxMensuel);
            }

            double calcul3 = calcul2 - 1;
            mensualite = calcul1 * (calcul2 / calcul3);

            return mensualite;
        }
};

void separation() {
    printf("+-----------------");
    for (int j = 0; j < COLS; j++) {
        printf("+--------------------");
    }
    printf("+\n");
}

int main() {
    double capital;
    cout << "Capital : ";
    cin >> capital;

    const char* banques[COLS] = {
        "Banque Populaire",
        "LCL",
        "Credit Agricole",
        "BNP Paribas"
    };

    int dure[3] = {10, 15, 20};
    double taux[2] = {3.0, 4.0};

   
    separation();
    printf("| %-15s ", "");
    for (int j = 0; j < COLS; j++)
        printf("| %-18s ", banques[j]);
    printf("|\n");
    separation();

    
    for (int t = 0; t < 2; t++) {

        
        printf("| Taux %d (%.0f%%)   ", t + 1, taux[t]);
        for (int j = 0; j < COLS; j++)
            printf("| %-18s ", "");
        printf("|\n");
        separation();

        
        for (int d = 0; d < 3; d++) {

            printf("| %-15d ", dure[d]);

            
            for (int b = 0; b < COLS; b++) {
                Emprunt e(capital, dure[d], taux[t]);
                printf("| %-18.2f ", e.calculerMensualite());
            }

            printf("|\n");
            separation();
        }
    }
