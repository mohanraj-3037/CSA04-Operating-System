#include <stdio.h>

int main(){
    int n,i,time=0,tq;
    int bt[10],rt[10],wt[10],tat[10];
    float awt=0, atat=0;

    printf("Enter number of processes: ");
    scanf("%d",&n);

    for(i=0;i<n;i++){
        printf("Enter BT P%d: ",i+1);
        scanf("%d",&bt[i]);
        rt[i] = bt[i];
        wt[i] = 0;
    }

    printf("Enter Time Quantum: ");
    scanf("%d",&tq);

    while(1){
        int done = 1;
        for(i=0;i<n;i++){
            if(rt[i] > 0){
                done = 0;
                if(rt[i] > tq){
                    time += tq;
                    rt[i] -= tq;
                }
                else{
                    time += rt[i];
                    wt[i] = time - bt[i];
                    rt[i] = 0;
                }
            }
        }
        if(done)
            break;
    }

    for(i=0;i<n;i++){
        tat[i] = wt[i] + bt[i];
        awt += wt[i];
        atat += tat[i];
    }

    printf("\nBT WT TAT\n");
    for(i=0;i<n;i++)
        printf("%d %d %d\n", bt[i], wt[i], tat[i]);

    printf("Avg WT = %.2f\nAvg TAT = %.2f", awt/n, atat/n);
    return 0;
}

