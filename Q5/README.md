
#include <stdio.h>
#include <ctype.h>

int word_count(const char s[])
{
    int count=0, i=0;

    while(s[i]!='\0')
    {
        if(!isspace(s[i]) &&
           (i==0 || isspace(s[i-1])))
            count++;

        i++;
    }

    return count;
}

int is_palindrome(const char s[])
{
    int left=0, right=0;

    while(s[right]!='\0')
        right++;

    right--;

    while(left<right)
    {
        if(!isalpha(s[left]))
        {
            left++;
            continue;
        }

        if(!isalpha(s[right]))
        {
            right--;
            continue;
        }

        if(tolower(s[left])!=tolower(s[right]))
            return 0;

        left++;
        right--;
    }

    return 1;
}

int main()
{
    printf("Words: %d\n",
    word_count("Meet at the library at 5 PM"));

    printf("%d %d\n",
    is_palindrome("Madam, I'm Adam"),
    is_palindrome("Hello"));

    return 0;
}

