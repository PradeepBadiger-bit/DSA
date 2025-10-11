MID TERM 
1]
#include <stdio.h>
#include <string.h>

#define DAYS 30
#define MAX_MEMBERS 50

struct Member {
    char name[50];
    int steps[DAYS];
};

void analyzeSteps(struct Member members[], int n) {
    for (int i = 0; i < n; i++) {
        int count = 0;
        int maxSteps = members[i].steps[0];

        for (int j = 0; j < DAYS; j++) {
            if (members[i].steps[j] > 10000)
                count++;
            if (members[i].steps[j] > maxSteps)
                maxSteps = members[i].steps[j];
        }

        printf("\nMember: %s\n", members[i].name);
        printf("Days exceeding 10,000 steps: %d\n", count);
        printf("Maximum step count in month: %d\n", maxSteps);
    }
}

int main() {
    int n;
    struct Member members[MAX_MEMBERS];

    printf("Enter number of members: ");
    scanf("%d", &n);
    getchar(); // consume newline

    for (int i = 0; i < n; i++) {
        printf("\nEnter name of member %d: ", i + 1);
        fgets(members[i].name, sizeof(members[i].name), stdin);
        members[i].name[strcspn(members[i].name, "\n")] = '\0'; // remove newline

        printf("Enter 30 days of step counts:\n");
        for (int j = 0; j < DAYS; j++) {
            scanf("%d", &members[i].steps[j]);
        }
    }

    analyzeSteps(members, n);

    return 0;
}


2]
#include <stdio.h>
#include <string.h>

#define DAYS 30
#define MAX_MEMBERS 50

struct Member {
    char name[50];
    int steps[DAYS];
};

void analyzeSteps(struct Member members[], int n) {
    for (int i = 0; i < n; i++) {
        int count = 0;
        int maxSteps = members[i].steps[0];

        for (int j = 0; j < DAYS; j++) {
            if (members[i].steps[j] > 10000)
                count++;
            if (members[i].steps[j] > maxSteps)
                maxSteps = members[i].steps[j];
        }

        printf("\nMember: %s\n", members[i].name);
        printf("Days exceeding 10,000 steps: %d\n", count);
        printf("Maximum step count in month: %d\n", maxSteps);
    }
}

int main() {
    int n;
    struct Member members[MAX_MEMBERS];

    printf("Enter number of members: ");
    scanf("%d", &n);
    getchar(); // consume newline

    for (int i = 0; i < n; i++) {
        printf("\nEnter name of member %d: ", i + 1);
        fgets(members[i].name, sizeof(members[i].name), stdin);
        members[i].name[strcspn(members[i].name, "\n")] = '\0'; // remove newline

        printf("Enter 30 days of step counts:\n");
        for (int j = 0; j < DAYS; j++) {
            scanf("%d", &members[i].steps[j]);
        }
    }

    analyzeSteps(members, n);

    return 0;
}
3]
#include <stdio.h>
#include <stdlib.h>

#define MAX 50

// Structure of a tree node
struct Node {
    char ch;
    int freq;
    struct Node *left, *right;
};

// Queue for level-order insertion
struct Queue {
    struct Node *arr[MAX];
    int front, rear;
};

// Queue functions
void initQueue(struct Queue *q) {
    q->front = q->rear = -1;
}

int isEmpty(struct Queue *q) {
    return q->front == -1;
}

void enqueue(struct Queue *q, struct Node *node) {
    if (q->rear == MAX - 1) return;
    if (q->front == -1) q->front = 0;
    q->arr[++q->rear] = node;
}

struct Node* dequeue(struct Queue *q) {
    if (isEmpty(q)) return NULL;
    struct Node *node = q->arr[q->front];
    if (q->front == q->rear)
        q->front = q->rear = -1;
    else
        q->front++;
    return node;
}

// Function to create new node
struct Node* createNode(char ch) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->ch = ch;
    newNode->freq = 1;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// Function to find and update existing character
int updateFrequency(struct Node *root, char ch) {
    if (root == NULL) return 0;
    if (root->ch == ch) {
        root->freq++;
        return 1;
    }
    return updateFrequency(root->left, ch) || updateFrequency(root->right, ch);
}

// Function to insert a new node in level order
void insertLevelOrder(struct Node **root, char ch) {
    // If root is empty, create new root
    if (*root == NULL) {
        *root = createNode(ch);
        return;
    }

    // If character already exists, update its frequency
    if (updateFrequency(*root, ch))
        return;

    // Otherwise, insert in the next available position
    struct Queue q;
    initQueue(&q);
    enqueue(&q, *root);

    while (!isEmpty(&q)) {
        struct Node *temp = dequeue(&q);

        if (temp->left == NULL) {
            temp->left = createNode(ch);
            break;
        } else
            enqueue(&q, temp->left);

        if (temp->right == NULL) {
            temp->right = createNode(ch);
            break;
        } else
            enqueue(&q, temp->right);
    }
}

// Function to print level-order traversal
void printLevelOrder(struct Node *root) {
    if (root == NULL) return;

    struct Queue q;
    initQueue(&q);
    enqueue(&q, root);

    while (!isEmpty(&q)) {
        struct Node *temp = dequeue(&q);
        printf("(%c,%d) ", temp->ch, temp->freq);

        if (temp->left) enqueue(&q, temp->left);
        if (temp->right) enqueue(&q, temp->right);
    }
}

// Main
int main() {
    struct Node *root = NULL;
    char str[100];

    printf("Enter a string: ");
    scanf("%s", str);

    for (int i = 0; str[i] != '\0'; i++) {
        insertLevelOrder(&root, str[i]);
    }

    printf("\nLevel-order traversal showing each character and its frequency:\n");
    print


    LAB EXAM 
    2]
    
