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
