//McKenna Branting
//Sites used for guidance: https://stackoverflow.com/questions/56139704/deadlocks-in-c-with-semaphores
// and https://www.bartleby.com/c-code.-dining-philosophers-problem-is-a-famous-problem-in-os.-a-deadlock-may-happen-when-all-philos/b4bc7b49-8ad2-4d64-a6ac-fc20608ed69d
/* 
        clock example: frequency of primes 
        original source code link:
        https://www.tutorialspoint.com/c_standard_library/c_function_clock.htm
*/
#include <stdio.h>      /* printf */
#include <time.h>       /* clock_t, clock, CLOCKS_PER_SEC */
#include <math.h>       /* sqrt */
#include <semaphore.h>
#include <pthread.h>
#include <unistd.h>
#define N 5 // number of activities being preformed

sem_t S[N]; //semaphores for actions

pthread_t tid[2]; //calling the Posix thread

int frequency_of_primes (int n) {
  int i,j;
  int freq=n-1;
  for (i=2; i<=n; ++i) for (j=(i)*(i);j>1;--j) if (i%j==0) {--freq; break;}
  return freq;
}


void * activity(void *num);
void take_action(int);
void give_action(int);

int act_num[N] = {0,1,2,3,4};

int main ()
{

//to calculate time 
    clock_t tStart, tStop, tPassed;
    int f;
    tStart = clock();
    printf ("Calculating...\n");
    f = frequency_of_primes (99999);
    printf ("The number of primes lower than 100,000 is: %d\n",f);

    int i;
    pthread_t thread_id[N];

    for(i=0;i<N;i++)
        sem_init(&S[i],0,1);

    for(i=0;i<N;i++)
        pthread_create(&thread_id[i],NULL,activity,&act_num[i]);

    for(i=0;i<N;i++)
        pthread_join(thread_id[i],NULL);

    tStop = clock();
    tPassed = tStop - tStart;
    printf ("It took me %ld clicks (%f seconds).\n",tPassed,((float)tPassed)/CLOCKS_PER_SEC);
    return 0;
    //calculate total time of components 

}

    void *activity(void *num) {
        while(1)
        {
            int *i = num;
            take_action(*i);
            give_action(*i);
        }
    }

    void take_action(int act_number) {
        printf("Activity %d needs an action\n",act_number);

        sem_wait(&S[act_number]); //take the left action
        printf("Activity %d takes action %d \n",act_number,act_number);

        sem_wait(&S[(act_number+1)%N]); //takes the right action
        printf("Activity %d takes action %d \n",act_number,(act_number+1)%N);
    
        printf("Philospher %d is eating\n",act_number);
        sleep(1);
    }

    void give_action(int act_number) {
        sem_post (&S[act_number]); //give the left action
        printf("Activity %d giving action %d \n",act_number,act_number);

        sleep(1);

        sem_post (&S[(act_number+1)%N]); //give the right action
        printf("Activity %d giving action %d \n",act_number,(act_number+1)%N);

        printf("Activity %d is loading\n",act_number);
        sleep(1);
    }

