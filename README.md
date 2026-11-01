# EMERGENCY-SERVICE-MANAGEMENT-SYSTEM 
#include <stdio.h>
#include <string.h>

#define MAX 100

struct Emergency {
    int id;
    char name[50];
    char type[30];
    char location[50];
    int priority;
};

struct Emergency queue[MAX];
int count = 0;
int nextId = 1;

// Add emergency request
void addEmergency() {
    if (count == MAX) {
        printf("\nEmergency Queue is Full!\n");
        return;
    }

    struct Emergency e;

    e.id = nextId++;

    printf("\nEnter Patient/Person Name: ");
    scanf(" %[^\n]", e.name);

    printf("Enter Emergency Type (Ambulance/Fire/Police): ");
    scanf(" %[^\n]", e.type);

    printf("Enter Location: ");
    scanf(" %[^\n]", e.location);

    printf("\nSelect Priority:\n");
    printf("1. Critical\n");
    printf("2. High\n");
    printf("3. Medium\n");
    printf("4. Low\n");
    printf("Enter Priority: ");
    scanf("%d", &e.priority);

    if (e.priority < 1 || e.priority > 4) {
        printf("Invalid Priority!\n");
        nextId--;
        return;
    }

    queue[count] = e;
    count++;

    printf("\nEmergency Request Added Successfully!");
    printf("\nEmergency ID: %d\n", e.id);
}

// Display all emergencies
void displayEmergencies() {
    if (count == 0) {
        printf("\nNo Emergency Requests Available!\n");
        return;
    }

    printf("\n========== EMERGENCY RECORDS ==========\n");

    for (int i = 0; i < count; i++) {
        printf("\nID: %d", queue[i].id);
        printf("\nName: %s", queue[i].name);
        printf("\nType: %s", queue[i].type);
        printf("\nLocation: %s", queue[i].location);

        printf("\nPriority: ");

        switch (queue[i].priority) {
            case 1: printf("Critical"); break;
            case 2: printf("High"); break;
            case 3: printf("Medium"); break;
            case 4: printf("Low"); break;
        }

        printf("\n-----------------------------------\n");
    }
}

// Process highest priority emergency
void processEmergency() {
    if (count == 0) {
        printf("\nNo Emergency to Process!\n");
        return;
    }

    int highest = 0;

    for (int i = 1; i < count; i++) {
        if (queue[i].priority < queue[highest].priority) {
            highest = i;
        }
    }

    printf("\n========== PROCESSING EMERGENCY ==========\n");
    printf("Emergency ID: %d\n", queue[highest].id);
    printf("Name: %s\n", queue[highest].name);
    printf("Type: %s\n", queue[highest].type);
    printf("Location: %s\n", queue[highest].location);

    printf("\nEmergency Successfully Processed!\n");

    // Remove processed emergency
    for (int i = highest; i < count - 1; i++) {
        queue[i] = queue[i + 1];
    }

    count--;
}

// Search emergency by ID
void searchEmergency() {
    int id, found = 0;

    printf("\nEnter Emergency ID to Search: ");
    scanf("%d", &id);

    for (int i = 0; i < count; i++) {
        if (queue[i].id == id) {
            printf("\nEmergency Found!\n");
            printf("ID: %d\n", queue[i].id);
            printf("Name: %s\n", queue[i].name);
            printf("Type: %s\n", queue[i].type);
            printf("Location: %s\n", queue[i].location);
            printf("Priority: %d\n", queue[i].priority);

            found = 1;
            break;
        }
    }

    if (!found) {
        printf("\nEmergency Record Not Found!\n");
    }
}

// Main function
int main() {
    int choice;

    do {
        printf("\n\n====================================");
        printf("\n   EMERGENCY SERVICE MANAGEMENT");
        printf("\n====================================");
        printf("\n1. Add Emergency Request");
        printf("\n2. Display All Emergencies");
        printf("\n3. Process Highest Priority Emergency");
        printf("\n4. Search Emergency by ID");
        printf("\n5. Exit");
        printf("\n====================================");

        printf("\nEnter Your Choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addEmergency();
                break;

            case 2:
                displayEmergencies();
                break;

            case 3:
                processEmergency();
                break;

            case 4:
                searchEmergency();
                break;

            case 5:
                printf("\nThank You for Using Emergency Service System!\n");
                break;

            default:
                printf("\nInvalid Choice! Try Again.\n");
        }

    } while (choice != 5);  

    return 0;
}
