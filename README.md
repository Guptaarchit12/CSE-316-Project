
#include <stdio.h>

int main() {

    int bt[20], p[20], wt[20], tat[20], priority[20], i, j, n, total = 0, pos, temp;

    float avg_wt, avg_tat;

    printf("Enter number of processes:");
    scanf("%d", &n);

    printf("\nEnter Estimated Time and Priority:\n");

    for (i = 0; i < n; i++) {
        printf("p%d:", i + 1);
        scanf("%d %d", &bt[i], &priority[i]);
        p[i] = i + 1; // contains process
    }

    // Sorting processes based on priority using selection sort
    for (i = 0; i < n - 1; i++) {
        pos = i;
        for (j = i + 1; j < n; j++) {
            if (priority[j] < priority[pos])
                pos = j;
        }
        temp = bt[i];
        bt[i] = bt[pos];
        bt[pos] = temp;
        temp = p[i];
        p[i] = p[pos];
        p[pos] = temp;
        temp = priority[i];
        priority[i] = priority[pos];
        priority[pos] = temp;
    }

    printf("\nSimulation of Process Execution:\n");
    for (i = 0; i < n; i++) {
        for (j = 0; j < bt[i]; j++) {
            printf("Time %d: p%d (Priority: %d)\n", j, p[i], priority[i]);
        }
    }

    wt[0] = 0; // waiting time for the first process will be zero

    // Calculate waiting time
    for (i = 1; i < n; i++) {
        wt[i] = 0;
        for (j = 0; j < i; j++) {
            wt[i] += bt[j];
        }
        total += wt[i];
    }

    avg_wt = (float)total / n; // average waiting time
    total = 0;

    printf("\nProcess\tEstimated Time\tPriority\tWaiting Time\tTurnaround Time");

    for (i = 0; i < n; i++) {
        tat[i] = bt[i] + wt[i]; // calculate turnaround time
        total += tat[i];
        printf("\np%d\t\t%d\t\t%d\t\t%d\t\t%d", p[i], bt[i], priority[i], wt[i], tat[i]);
    }

    avg_tat = (float)total / n; // average turnaround time

    printf("\n\nAverage Waiting Time=%f", avg_wt);
    printf("\nAverage Turnaround Time=%f\n", avg_tat);

    return 0;
}
