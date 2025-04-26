include <stdio.h>
#include <stdlib.h>
#ifdef _WIN32
#include <windows.h>
#else
#include <unistd.h>
#end if


void delay(int milliseconds) {
#ifdef _WIN32
    Sleep((DWORD)milliseconds);
#else
    usleep(milliseconds * 1000); 
#endif
}

int main() {
    int minutes, seconds;

    printf("Enter the timer duration (in minutes and seconds, separated by a space): ");
    if (scanf("%d %d", &minutes, &seconds) != 2 || minutes < 0 || seconds < 0 || seconds >= 60) {
        printf("Invalid input. Please enter a valid time in minutes and seconds.\n");
        return 1;
    }

    int total_seconds = (minutes * 60) + seconds;

    printf("Timer set for %d minutes and %d seconds.\n", minutes, seconds);

    while (total_seconds > 0) {
        int current_minutes = total_seconds / 60;
        int current_seconds = total_seconds % 60;

        printf("\rTime remaining: %02d:%02d", current_minutes, current_seconds);
        fflush(stdout); 

        delay(1000);
        total_seconds--;
    }

    printf("\n\n********************\n");
    printf("* TIME'S UP!   *\n");
    printf("********************\n");

    

    return 0;
}
