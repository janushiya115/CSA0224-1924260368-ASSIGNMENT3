
#include <stdio.h>

int main()
{
    int rain[3][4] = {
        {100, 120, 80, 90},
        {50, 60, 40, 70},
        {150, 130, 160, 140}
    };

    int i, j, max = 0, total;
    int totalRain = 0;

    for(i = 0; i < 3; i++)
    {
        total = 0;

        for(j = 0; j < 4; j++)
        {
            total += rain[i][j];
            totalRain += rain[i][j];

            if(rain[i][j] > max)
                max = rain[i][j];
        }

        printf("District %d Total = %d\n", i+1, total);
    }

    printf("State Average = %.2f\n", totalRain/12.0);
    printf("Maximum Rainfall = %d\n", max);

    return 0;
}

