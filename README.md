# Bus-Route-Finder
A C-based Bus Route Finder that reads bus numbers and route stops from a text file and allows users to search for buses passing through a specified starting point. It uses structures, file handling, string functions, and user input to efficiently identify matching bus routes.
#include <stdio.h>
#include <string.h>
struct Bus {
    char number[20];
    char stops[500];
};
int main() {
    struct Bus b[50];
    int i = 0, count = 0;
    char search[50];
    FILE *fp;
    fp = fopen("busdata.txt", "r");
    if (fp == NULL) {
        printf("Error opening file!\n");
        return 1;
    }
        while (fscanf(fp, "%s", b[i].number) != EOF) {
        fgetc(fp);  
        fgets(b[i].stops, sizeof(b[i].stops), fp);
        b[i].stops[strcspn(b[i].stops, "\n")] = '\0'; 
        i++;
        count++;
    }
    fclose(fp);
    printf("Enter the starting point: ");
    scanf("%s", search);
   printf("\nBuses passing through %s:\n", search);
   int found = 0;
    for (i = 0; i < count; i++) {
        if (strstr(b[i].stops, search) != NULL) {
            printf("%s\n", b[i].number);
            found = 1;
        }
    }
    if (!found) {
        printf("No buses found.\n");
    }
    return 0;
}
