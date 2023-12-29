# E_cars
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAX_voitures 100
#define MAX_locations 50
struct voiture {
    int id;
    char marque[50];
    char modele[50];
    char etat[20];
    
} ;

struct location {
    int idVoiture;
    char date[20];
};


struct voiture ajouter_une_voiture() {
    
    struct voiture v;
    printf("Donner id de la voiture : ");
    scanf("%d", &v.id);
    printf("Donner la marque de la voiture : ");
    scanf("%s", &v.marque);
    printf("Donner le modele de la voiture : ");
    scanf("%s", &v.modele);
    printf("Donner l'etat de la voiture : ");
    scanf("%s", &v.etat);
    return v;
    
}
struct location ajouter_location() {
    struct location l;
    printf("Donner id de la voiture : ");
    scanf("%d", &l.idVoiture);
    printf("Donner la date de la location : ");
    scanf("%s", &l.date);
    return l;
}
void afficherVoituresDisponibles( int nbVoitures) {
    printf("\nVoitures disponibles :\n");
    
    if (nbVoitures == 0) {
        printf("Aucune voiture disponible.\n");
    } else {
        printf("%-5s %-15s %-15s %-10s\n", "ID", "Marque", "Modèle", "État");
        printf("-----------------------------------------\n");

        
        }
    }
void louerVoiture(int nbVoitures,int nbLocations) {
    int idVoiture;
    char date[20]; 
    printf("\nVoitures disponibles pour la location :\n");
    printf("%-5s %-15s %-15s %-10s\n", "ID", "Marque", "Modèle", "État");
    printf("-----------------------------------------\n");

}

  
int main() {
    struct voiture voitures[MAX_voitures];
    struct location locations[MAX_locations];
    int choice;
    int nbVoitures = 0;
    int nbLocations = 0;

    do {
        printf("\nMenu:\n");
        printf("1. Ajouter une voiture\n");
        printf("2. Ajouter une location\n");
        printf("3. Afficher voitures disponibles\n");
        printf("4. Afficher historique d'une journée\n");
        printf("5. Afficher historique d'un mois\n");
        printf("6. Louer une voiture\n");
        printf("7. Afficher description d'une voiture\n");
        printf("8. Supprimer voiture en panne\n");
        
        printf("0. Quitter\n");

        printf("Choix : ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                voitures[nbVoitures+1]=ajouter_une_voiture();
                nbVoitures++;
                break;
            case 2:
                locations[nbLocations+1]=ajouter_location();
                nbLocations++;
                break;
            case 3:
                afficherVoituresDisponibles(nbVoitures);
                
                for (int i = 0; i < nbVoitures; i++) {
                     if (strcmp(voitures[i].etat, "Disponible") == 0) {
                       printf("%-5d %-15s %-15s %-10s\n",
                       voitures[i].id, voitures[i].marque, voitures[i].modele, voitures[i].etat);
            }
                }
                break;
            case 4:
                 char dateRecherche[20];

             printf("\nAfficher l'historique pour une journée spécifique :\n");
                printf("Entrez la date (au format JJ/MM/AAAA) : ");
               scanf("%s", dateRecherche);

            printf("\nHistorique des locations pour le %s :\n", dateRecherche);
               printf("%-5s %-10s\n", "ID Voiture", "Date");
                 printf("--------------------\n");
                 int historiqueTrouve = 0;

                for (int i = 0; i < nbLocations; i++) {
                   if (strcmp(locations[i].date, dateRecherche) == 0) {
                   printf("%-12d %-10s\n", locations[i].idVoiture, locations[i].date);
                   historiqueTrouve = 1;
                   if (!historiqueTrouve) {
                  printf("Aucune location trouvée pour la date spécifiée.\n");
    }
        }}
                break;
            case 5:
                  char moisRecherche[8];

    printf("\nAfficher l'historique pour un mois spécifique :\n");
    printf("Entrez le mois (au format MM/AAAA) : ");
    scanf("%s", moisRecherche);

    printf("\nHistorique des locations pour le mois %s :\n", moisRecherche);
    printf("%-5s %-10s\n", "ID Voiture", "Date");
    printf("--------------------\n");
                    for (int i = 0; i < nbLocations; i++) {
                       char moisLocation[8];
                       strncpy(moisLocation, locations[i].date + 3, 7);

                       if (strcmp(moisLocation, moisRecherche) == 0) {
                       printf("%-12d %-10s\n", locations[i].idVoiture, locations[i].date);
                       historiqueTrouve = 1;
        }
    }

                 if (!historiqueTrouve) {
                     printf("Aucune location trouvée pour le mois spécifié.\n");
    }
                break;
            case 6:
                louerVoiture(nbVoitures,nbLocations);
                    for (int i = 0; i < nbVoitures; i++) {
                     if (strcmp(voitures[i].etat, "Disponible") == 0) {
                        printf("%-5d %-15s %-15s %-10s\n",
                   voitures[i].id, voitures[i].marque, voitures[i].modele, voitures[i].etat);
        }
    }
            int idVoiture;
             printf("Entrez l'ID de la voiture que vous souhaitez louer : ");
             scanf("%d", &idVoiture);
             int voitureExiste = 0;
              for (int i = 0; i < nbVoitures; i++) {
               if (voitures[i].id == idVoiture && strcmp(voitures[i].etat, "Disponible") == 0) {
            voitureExiste = 1;
            break;
        }
    }

    if (voitureExiste) {
        locations[nbLocations].idVoiture = idVoiture;
        char date;
        printf("Entrez la date de location (au format JJ/MM/AAAA) : ");
        scanf("%s", date);
        strcpy(locations[nbLocations].date, date);
        for (int i = 0; i < nbVoitures; i++) {
            if (voitures[i].id == idVoiture) {
                strcpy(voitures[i].etat, "Louée");
                break;
            }
        }
        (nbLocations)++;

        printf("La voiture a été louée avec succès.\n");
    } else {
        printf("Voiture non disponible ou ID invalide.\n");
    }
                break;
            case 7:
                {int idVoiture;
                printf("Entrez l'ID de la voiture pour afficher la description : ");
                scanf("%d", &idVoiture);
                
                      int voitureTrouvee = 0;

                    for (int i = 0; i < nbVoitures; i++) {
                        if (voitures[i].id == idVoiture) {
                         voitureTrouvee = 1;

            printf("\nDescription de la voiture (ID %d) :\n", idVoiture);
            printf("%-10s %-15s\n", "Marque", "Modèle");
            printf("--------------------\n");
            printf("%-10s %-15s\n", voitures[i].marque, voitures[i].modele);
            printf("\nÉtat : %s\n", voitures[i].etat);

            break;
        }
    }

    if (!voitureTrouvee) {
        printf("Aucune voiture trouvée avec l'ID spécifié.\n");
    }
                }
                break;
            case 8:
                    
                     int voitureTrouvee = 0;

                   printf("\nSupprimer une voiture en panne :\n");
                  printf("Entrez l'ID de la voiture à supprimer : ");
                   scanf("%d", &idVoiture);

              for (int i = 0; i < nbVoitures; i++) {
        if (voitures[i].id == idVoiture && strcmp(voitures[i].etat, "Panne") == 0) {
            for (int j = i; j < nbVoitures - 1; j++) {
                voitures[j] = voitures[j + 1];
            }

            (nbVoitures)--;
            voitureTrouvee = 1;
            printf("La voiture en panne a été supprimée avec succès.\n");
            break;
        }
    }
                break;
            
            
            case 0:
                printf("Au revoir !\n");
                break;
            default:
                printf("Choix invalide. Veuillez réessayer.\n");
        }

    } while (choice != 0);

    return 0;
}
