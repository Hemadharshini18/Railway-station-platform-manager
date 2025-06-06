# Railway-station-platform-manager
Railway station platform manager using data structure
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAX 5 // Max number of trains on platform
typedef struct {
 int train_no;
 char train_name[50];
 char schedule[50];
} Train;
Train queue[MAX];
int front = -1, rear = -1;
// Check if queue is full
int isFull() {
 return rear == MAX - 1;
}
// Check if queue is empty
int isEmpty() {
 return front == -1 || front > rear;
}
// Add train to queue (assign to platform)
void enqueue() {
 if (isFull()) {
 printf("Platform is full! Cannot assign more trains.\n");
 return;
 }
 Train t;
 printf("Enter train number: ");
 scanf("%d", &t.train_no);
 printf("Enter train name: ");
 scanf(" %[^\n]", t.train_name);
 printf("Enter schedule: ");
 scanf(" %[^\n]", t.schedule);
 if (front == -1) front = 0;
 rear++;
 queue[rear] = t;
 printf("Train assigned to platform position %d.\n", rear + 1);
}
// Remove train from queue (train departs)
void dequeue() {
 if (isEmpty()) {
 printf("No train to remove. Platform is empty.\n");
 return;
 }
 printf("Train %d (%s) departing from platform.\n",
 queue[front].train_no, queue[front].train_name);
 front++;
}
// Display train at front of queue
void check_front() {
 if (isEmpty()) {
 printf("Platform is empty.\n");
 } else {
 printf("Next train to depart: %d (%s), Schedule: %s\n",
 queue[front].train_no, queue[front].train_name, queue[front].schedule);
 }
}
// Display all trains on platform
void display_queue() {
 if (isEmpty()) {
 printf("Platform is empty.\n");
 return;
 }
 printf("\n--- Platform Status ---\n");
 for (int i = front; i <= rear; i++) {
 printf("Position %d: Train %d (%s), Schedule: %s\n",
 i + 1, queue[i].train_no, queue[i].train_name, queue[i].schedule);
 }
}
// Update schedule of a train
void update_schedule() {
 if (front == -1 || front > rear) {
 printf("No trains on platform.\n");
 return;
 }
 int num, found = 0;
 printf("Enter train number to update schedule: ");
 scanf("%d", &num);
 for (int i = front; i <= rear; i++) {
 printf("Checking train number: %d\n", queue[i].train_no); // debug line
 if (queue[i].train_no == num) {
 while (getchar() != '\n');
 printf("Enter new schedule: ");
 scanf(" %[^\n]", queue[i].schedule);
 printf("Schedule updated.\n");
 found = 1;
 break;
 }
 }
 if (!found) {
 printf("Train not found.\n");
 }
}
int main() {
 int choice;
 while (1) {
 printf("\n--- Railway Platform Manager ---\n");
 printf("1. Assign new train to platform\n");
 printf("2. Update train schedule\n");
 printf("3. Remove train from platform\n");
 printf("4. Check train on platform\n");
 printf("5. Display platform status\n");
 printf("6. Exit\n");
 printf("Enter your choice: ");
 scanf("%d", &choice);
 switch (choice) {
 case 1: enqueue(); break;
 case 2: update_schedule(); break;
 case 3: dequeue(); break;
 case 4: check_front(); break;
 case 5: display_queue(); break;
 case 6:
 printf("Exiting Railway Platform Manager.\n");
 exit(0);
 default:
 printf("Invalid choice. Please enter a number from 1 to 6.\n");
 }
 }
 return 0;
}


