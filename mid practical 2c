#include <stdio.h>
#include <stdlib.h>

#define MAX 5

typedef struct {
    int items[MAX];
    int front, rear;
} CircularQueue;

// Helper function to check if a customer ID is already in the queue
int isCustomerInQueue(CircularQueue* q, int customerId) {
    if (q->front == -1) {
        return 0; // Queue is empty
    }
    for (int i = q->front; ; i = (i + 1) % MAX) {
        if (q->items[i] == customerId) {
            return 1; // Customer ID found in the queue
        }
        if (i == q->rear) break;
    }
    return 0; // Customer ID not found
}

// Adds a customer ID to the queue.
void addCall(CircularQueue* q, int customerId) {
    if (isCustomerInQueue(q, customerId)) {
        printf("-> ERROR: Customer %d is already in the queue.\n", customerId);
        return;
    }
    if ((q->rear + 1) % MAX == q->front) {
        printf("-> ERROR: Queue is full. Please wait.\n");
        return;
    }
    if (q->front == -1) q->front = 0; // First element
    q->rear = (q->rear + 1) % MAX;
    q->items[q->rear] = customerId;
    printf("-> SUCCESS: Call added for customer %d.\n", customerId);
}

// Removes the next customer ID from the queue.
void removeCall(CircularQueue* q) {
    if (q->front == -1) {
        printf("-> INFO: Queue is empty. No customers to serve.\n");
        return;
    }
    printf("-> SUCCESS: Removed customer %d.\n", q->items[q->front]);
    if (q->front == q->rear) { // Was the last element
        q->front = q->rear = -1;
    } else {
        q->front = (q->front + 1) % MAX;
    }
}

// Displays all customer IDs currently in the queue.
void displayQueue(CircularQueue* q) {
    printf("--- Current Call Queue ---\n");
    if (q->front == -1) {
        printf("   (Queue is empty)\n");
        return;
    }
    printf("   Customers waiting: ");
    for (int i = q->front; ; i = (i + 1) % MAX) {
        printf("%d ", q->items[i]);
        if (i == q->rear) break;
    }
    printf("\n   (Front of queue is %d)\n", q->items[q->front]);
}

int main() {
    CircularQueue q = {.front = -1, .rear = -1}; // Initialize queue directly
    int choice = 0, customerId = 0;

    while (choice != 4) {
        printf("\n--- Call Center Menu ---\n"
            "1. Add Call | 2. Remove Call | 3. Display Queue | 4. Exit\n"
            "Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("   Enter customer ID to add: ");
                scanf("%d", &customerId);
                addCall(&q, customerId);
                break;
            case 2: removeCall(&q); break;
            case 3: displayQueue(&q); break;
            case 4: printf("Exiting program. Goodbye!\n"); break;
            default: printf("-> ERROR: Invalid choice.\n"); break;
        }
    }
    return 0;
}
