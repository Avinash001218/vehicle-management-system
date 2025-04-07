# vehicle-management-system
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
typedef struct Vehicle
{
    char vehicleNo[10];
    char vehicleType[20];
    char ownerName[30];
    char contactNo[15];
    struct Vehicle* next;
} 
Vehicle;
Vehicle* createNode();
void insertVehicle(Vehicle** head);
void displayVehicles(Vehicle* head);
void searchVehicle(Vehicle* head);
void deleteVehicle(Vehicle** head);

int main() {
    Vehicle* head = NULL;
    int choice;

    while (1) {
        printf("Vehicle Management System\n");
        printf("1. Insert Vehicle\n");
        printf("2. Display Vehicles\n");
        printf("3. Search Vehicle\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
            case 1:
                insertVehicle(&head);
                break;
            case 2:
                displayVehicles(head);
                break;
            case 3:
                searchVehicle(head);
                break;
            case 5:
                exit(0);
            default:
                printf("Invalid choice!\n");
        }
    }

    return 0;
}

// Create a new node
Vehicle* createNode()
{
    Vehicle* newNode = (Vehicle*) malloc(sizeof(Vehicle));
    if (!newNode) {
        printf("Memory error!\n");
        return NULL;
    }

    printf("Enter vehicle number: ");
    scanf("%s", newNode->vehicleNo);
    printf("Enter vehicle type: ");
    scanf("%s", newNode->vehicleType);
    printf("Enter owner's name: ");
    scanf("%s", newNode->ownerName);
    printf("Enter contact number: ");
    scanf("%s", newNode->contactNo);
    newNode->next = NULL;

    return newNode;
}

// Insert vehicle into linked list
void insertVehicle(Vehicle** head) {
    Vehicle* newNode = createNode();

    if (*head == NULL) {
        *head = newNode;
    } else {
        Vehicle* temp = *head;
        while (temp->next) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}

// Display all vehicles
void displayVehicles(Vehicle* head) {
    if (head == NULL) {
        printf("No vehicles found!\n");
    } else {
        printf("Vehicle List:\n");
        while (head) {
            printf("Vehicle No: %s\n", head->vehicleNo);
            printf("Vehicle Type: %s\n", head->vehicleType);
            printf("Owner's Name: %s\n", head->ownerName);
            printf("Contact No: %s\n\n", head->contactNo);
            head = head->next;
        }
    }
}

// Search vehicle by number
void searchVehicle(Vehicle* head) {
    char vehicleNo[10];
    printf("Enter vehicle number to search: ");
    scanf("%s", vehicleNo);

    while (head) {
        if (strcmp(head->vehicleNo, vehicleNo) == 0) {
            printf("Vehicle found!\n");
            printf("Vehicle No: %s\n", head->vehicleNo);
            printf("Vehicle Type: %s\n", head->vehicleType);
            printf("Owner's Name: %s\n", head->ownerName);
            printf("Contact No: %s\n", head->contactNo);
            return;
        }
        head = head->next;
    }

    printf("Vehicle not found!\n");
}

// Delete vehicle by number
void deleteVehicle(Vehicle** head)
{
    char vehicleNo[10];
    printf("Enter vehicle number to delete: ");
    scanf("%s", vehicleNo);

    if (*head == NULL)
    {
        printf("No vehicles found!\n");
    } else if (strcmp((*head)->vehicleNo, vehicleNo) == 0)
    {
        Vehicle* temp = *head;
        *head = (*head)->next;
        free(temp);
        printf("Vehicle deleted!\n");
    } else {
        Vehicle* prev = *head;
        Vehicle* curr = (*head)->next;
        while (curr) {
            if (strcmp(curr->vehicleNo, vehicleNo) == 0)
            {
                prev->next = curr->next;
                free(curr);
                printf("Vehicle deleted!\n");
                return;
            }
            prev = curr;
            curr = curr->next;
        }
        printf("Vehicle not found!\n");
    }
}
    
