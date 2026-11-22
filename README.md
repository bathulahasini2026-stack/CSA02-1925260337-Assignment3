1. COLLEGE CENTRAL LIBRARY – BINARY SEARCH

C CODE

#include <stdio.h>
int steps;

int binary_search(const int a[], int n, int key)
{
    steps = 0;
    int low = 0, high = n - 1;

    while (low <= high)
    {
        int mid = low + (high - low) / 2;
        steps++;

        if (a[mid] == key)
            return mid;
        else if (a[mid] < key)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return -1;
}

int main(void)
{
    int accession[] = {1021, 1048, 1103, 1190, 1222,
                       1305, 1377, 1402, 1460, 1533};
    int n = sizeof accession / sizeof accession[0];
    int keys[] = {1021, 1305, 1533, 1400};

    for (int k = 0; k < 4; k++)
    {
        int pos = binary_search(accession, n, keys[k]);
        printf("Book %d -> index %d, comparisons = %d\n",
               keys[k], pos, steps);
    }
    return 0;
}

PSEUDOCODE
1. Set steps = 0.
2. Set low = 0 and high = n - 1.
3. While low <= high:
   a. Calculate mid = low + (high - low) / 2.
   b. Increase steps by 1.
   c. If a[mid] equals key, return mid.
   d. If a[mid] is less than key, set low = mid + 1.
   e. Otherwise, set high = mid - 1.
4. If the search ends, return -1.

EXPECTED OUTPUT
Book 1021 -> index 0, comparisons = 3
Book 1305 -> index 5, comparisons = 3
Book 1533 -> index 9, comparisons = 4
Book 1400 -> index -1, comparisons = 4

2. EXAMINATION SEATING – INSERTION SORT

C CODE

#include <stdio.h>

int main(void)
{
    int a[100], n, i, j, key;

    printf("Enter number of students: ");
    scanf("%d", &n);

    if (n < 1 || n > 100)
    {
        printf("Invalid number of students\n");
        return 0;
    }

    printf("Enter register numbers:\n");
    for (i = 0; i < n; i++)
        scanf("%d", &a[i]);

    for (i = 1; i < n; i++)
    {
        key = a[i];
        j = i - 1;

        while (j >= 0 && a[j] > key)
        {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = key;
    }

    printf("Sorted register numbers:\n");
    for (i = 0; i < n; i++)
        printf("%d ", a[i]);

    return 0;
}

PSEUDOCODE
1. Read the number of students n.
2. Read n register numbers into array a.
3. For i from 1 to n - 1:
   a. Set key = a[i] and j = i - 1.
   b. While j >= 0 and a[j] > key:
      - Move a[j] one position to the right.
      - Decrease j by 1.
   c. Place key at a[j + 1].
4. Display the sorted register numbers.

SAMPLE INPUT
5
105 102 104 101 103

EXPECTED OUTPUT
101 102 103 104 105

COMPLEXITY
Best case: O(n). Average and worst case: O(n^2). Extra space: O(1).

3. INTER-CAMPUS ADMISSION – MERGE TWO DESCENDING ARRAYS

C CODE

#include <stdio.h>

int main(void)
{
    int a[100], b[100], c[200];
    int n, m, i, j, k = 0;

    printf("Enter number of students in Campus 1: ");
    scanf("%d", &n);
    printf("Enter Campus 1 scores in descending order:\n");
    for (i = 0; i < n; i++)
        scanf("%d", &a[i]);

    printf("Enter number of students in Campus 2: ");
    scanf("%d", &m);
    printf("Enter Campus 2 scores in descending order:\n");
    for (j = 0; j < m; j++)
        scanf("%d", &b[j]);

    i = 0;
    j = 0;

    while (i < n && j < m)
    {
        if (a[i] >= b[j])
            c[k++] = a[i++];
        else
            c[k++] = b[j++];
    }

    while (i < n)
        c[k++] = a[i++];

    while (j < m)
        c[k++] = b[j++];

    printf("Combined merit list:\n");
    for (i = 0; i < k; i++)
        printf("%d ", c[i]);

    return 0;
}

PSEUDOCODE
1. Read the sizes n and m of the two merit lists.
2. Read both arrays in descending order.
3. Initialize i = 0, j = 0 and k = 0.
4. While both arrays still contain elements:
   a. Compare a[i] and b[j].
   b. Copy the larger score into c[k].
   c. Advance the index of the copied array and increment k.
5. Copy any remaining elements from array a.
6. Copy any remaining elements from array b.
7. Display the combined array.

SAMPLE INPUT
Campus 1: 98 95 90 85 80
Campus 2: 99 96 91 82

EXPECTED OUTPUT
99 98 96 95 91 90 85 82 80

COMPLEXITY
Time: O(n + m). Extra space: O(n + m).

4. STATE DISASTER MANAGEMENT – 2D RAINFALL ARRAY

C CODE

#include <stdio.h>

int main(void)
{
    float rain[38][12];
    float annual[38] = {0};
    float monthlyTotal[12] = {0};
    float grandTotal = 0, maxRain = -1;
    float stateMonthlyAverage, averageAnnualPerDistrict;
    int wetDistrict = 0, wetMonth = 0;
    int i, j;

    printf("Enter rainfall for 38 districts and 12 months:\n");

    for (i = 0; i < 38; i++)
    {
        for (j = 0; j < 12; j++)
        {
            scanf("%f", &rain[i][j]);
            annual[i] += rain[i][j];
            monthlyTotal[j] += rain[i][j];
            grandTotal += rain[i][j];

            if (rain[i][j] > maxRain)
            {
                maxRain = rain[i][j];
                wetDistrict = i;
                wetMonth = j;
            }
        }
    }

    printf("\nAnnual rainfall totals:\n");
    for (i = 0; i < 38; i++)
        printf("District %d = %.2f mm\n", i + 1, annual[i]);

    stateMonthlyAverage = grandTotal / (38.0 * 12.0);
    averageAnnualPerDistrict = grandTotal / 38.0;

    printf("\nState monthly average rainfall = %.2f mm\n",
           stateMonthlyAverage);
    printf("Wettest district = %d\n", wetDistrict + 1);
    printf("Wettest month = %d\n", wetMonth + 1);
    printf("Maximum rainfall = %.2f mm\n", maxRain);

    printf("\nDistricts below 60%% of state average annual rainfall:\n");
    for (i = 0; i < 38; i++)
    {
        if (annual[i] < 0.60 * averageAnnualPerDistrict)
            printf("District %d\n", i + 1);
    }

    return 0;
}

PSEUDOCODE
1. Declare rain[38][12] and initialize annual totals and monthly totals to zero.
2. Read rainfall for each of 38 districts and 12 months.
3. For every reading:
   a. Add it to that district's annual total.
   b. Add it to that month's state total.
   c. Add it to the grand total.
   d. Update the wettest district and month if this reading is the largest.
4. Display the annual total for each district.
5. Calculate state monthly average = grand total / 456.
6. Calculate average annual rainfall per district = grand total / 38.
7. Display the wettest district, month and rainfall.
8. Display districts whose annual total is below 60% of the average annual rainfall per district.

NOTE
The 60% threshold is interpreted as 60% of the state's average annual rainfall per district. If your teacher intends 60% of the state monthly average, the comparison formula must be changed.

5. SMS FEEDBACK ANALYSER – WITHOUT string.h (TODO 1 AND TODO 2)

C CODE

#include <stdio.h>
#include <ctype.h>

int word_count(const char s[])
{
    int count = 0, inside = 0;

    for (int i = 0; s[i] != '\0'; i++)
    {
        if (s[i] != ' ')
        {
            if (inside == 0)
            {
                count++;
                inside = 1;
            }
        }
        else
            inside = 0;
    }
    return count;
}

int is_palindrome(const char s[])
{
    int left = 0, right = 0;

    while (s[right] != '\0')
        right++;
    right--;

    while (left < right)
    {
        while (left < right &&
               !isalpha((unsigned char)s[left]))
            left++;

        while (left < right &&
               !isalpha((unsigned char)s[right]))
            right--;

        if (tolower((unsigned char)s[left]) !=
            tolower((unsigned char)s[right]))
            return 0;

        left++;
        right--;
    }
    return 1;
}

int main(void)
{
    printf("Words: %d\n",
           word_count(" Meet at the library at 5 PM "));
    printf("%d %d\n",
           is_palindrome("Madam, I'm Adam"),
           is_palindrome("Hello"));
    return 0;
}

PSEUDOCODE – TODO 1: WORD COUNT
1. Initialize count = 0 and inside = 0.
2. Scan characters until the null character.
3. If the current character is not a space and inside is 0:
   - Increase count.
   - Set inside = 1.
4. If the current character is a space, set inside = 0.
5. Return count.

PSEUDOCODE – TODO 2: PALINDROME
1. Set left = 0 and find the last character using right.
2. While left is less than right:
   a. Move left forward past non-letter characters.
   b. Move right backward past non-letter characters.
   c. Compare the two letters after converting them to lowercase.
   d. If they differ, return 0.
   e. Move left forward and right backward.
3. Return 1 if no mismatch is found.

EXPECTED OUTPUT
Words: 7
1 0

NOTE
This solution does not use string.h. It uses ctype.h for isalpha() and tolower().

6. HOSTEL RESIDENT DIRECTORY – SORT, SEARCH AND DUPLICATES

C CODE

#include <stdio.h>
#include <string.h>

int main(void)
{
    char names[500][30], temp[30], key[30];
    int n, i, j, found = 0;

    printf("Enter number of residents: ");
    scanf("%d", &n);

    if (n < 1 || n > 500)
    {
        printf("Invalid number of residents\n");
        return 0;
    }

    printf("Enter resident names (one per line):\n");
    for (i = 0; i < n; i++)
        scanf(" %29[^
]", names[i]);

    // Alphabetical Bubble Sort
    for (i = 0; i < n - 1; i++)
    {
        for (j = 0; j < n - i - 1; j++)
        {
            if (strcmp(names[j], names[j + 1]) > 0)
            {
                strcpy(temp, names[j]);
                strcpy(names[j], names[j + 1]);
                strcpy(names[j + 1], temp);
            }
        }
    }

    printf("\nNames in alphabetical order:\n");
    for (i = 0; i < n; i++)
        printf("%s\n", names[i]);

    printf("\nEnter name to search: ");
    scanf(" %29[^
]", key);

    for (i = 0; i < n; i++)
    {
        if (strcmp(names[i], key) == 0)
        {
            printf("Resident found at position %d\n", i + 1);
            found = 1;
            break;
        }
    }

    if (!found)
        printf("Resident not found\n");

    printf("\nDuplicate names:\n");
    found = 0;

    for (i = 0; i < n - 1; i++)
    {
        if (strcmp(names[i], names[i + 1]) == 0)
        {
            printf("%s\n", names[i]);
            found = 1;

            while (i < n - 1 &&
                   strcmp(names[i], names[i + 1]) == 0)
                i++;
        }
    }

    if (!found)
        printf("No duplicate names found\n");

    return 0;
}

PSEUDOCODE
1. Read the number of residents n and validate that 1 <= n <= 500.
2. Read all resident names.
3. Sort names alphabetically using Bubble Sort:
   a. Compare adjacent names using strcmp().
   b. If the first name comes after the second, swap them using strcpy().
4. Display the sorted names.
5. Read the search name.
6. Compare it with each name using strcmp().
7. Display the position if found; otherwise display not found.
8. Scan adjacent sorted names to identify duplicates.
9. Display each duplicate name once.
10. Stop.

SAMPLE INPUT
6
Ravi
Anu
Kiran
Anu
Zoya
Bala
Search name: Kiran

EXPECTED OUTPUT
Anu
Anu
Bala
Kiran
Ravi
Zoya
Resident found at position 4
Duplicate names:
Anu

COMPLEXITY
Sorting: O(n^2). Searching: O(n). Duplicate scan: O(n).

7. STUDENT COUNCIL ELECTION – VOTE COUNT, SORT AND TIE

C CODE

#include <stdio.h>

int main(void)
{
    int votes[5000], count[12] = {0}, order[12];
    int n, candidates, valid = 0, invalid = 0;
    int i, j, temp, maxVotes = 0, tie = 0;

    printf("Enter number of candidates: ");
    scanf("%d", &candidates);
    printf("Enter number of votes: ");
    scanf("%d", &n);

    if (candidates < 1 || candidates > 12 ||
        n < 0 || n > 5000)
    {
        printf("Invalid input limits\n");
        return 0;
    }

    printf("Enter votes:\n");
    for (i = 0; i < n; i++)
    {
        scanf("%d", &votes[i]);

        if (votes[i] >= 1 && votes[i] <= candidates)
        {
            count[votes[i] - 1]++;
            valid++;
        }
        else
            invalid++;
    }

    for (i = 0; i < candidates; i++)
        if (count[i] > maxVotes)
            maxVotes = count[i];

    for (i = 0; i < candidates; i++)
        if (count[i] == maxVotes)
            tie++;

    for (i = 0; i < candidates; i++)
        order[i] = i;

    // Sort candidate indices by vote count, descending
    for (i = 0; i < candidates - 1; i++)
    {
        for (j = 0; j < candidates - i - 1; j++)
        {
            if (count[order[j]] < count[order[j + 1]])
            {
                temp = order[j];
                order[j] = order[j + 1];
                order[j + 1] = temp;
            }
        }
    }

    printf("\nValid votes = %d\n", valid);
    printf("Invalid votes = %d\n", invalid);
    printf("\nCandidate vote counts (descending):\n");

    for (i = 0; i < candidates; i++)
        printf("Candidate %d = %d\n",
               order[i] + 1, count[order[i]]);

    if (valid == 0)
        printf("\nNo valid votes. No winner.\n");
    else if (tie > 1)
    {
        printf("\nElection result: TIE\n");
        printf("Tied candidates: ");
        for (i = 0; i < candidates; i++)
            if (count[i] == maxVotes)
                printf("%d ", i + 1);
        printf("\n");
    }
    else
        printf("\nWinner: Candidate %d\n", order[0] + 1);

    return 0;
}

PSEUDOCODE
1. Read candidate count and vote count; validate their limits.
2. Initialize each candidate's vote count to zero.
3. Read each vote:
   a. If the vote is from 1 to the candidate count, increment that candidate's count and valid count.
   b. Otherwise, increment invalid count.
4. Find the maximum vote count.
5. Count how many candidates have the maximum.
6. Initialize an order array with candidate indices.
7. Sort the order array by candidate vote totals in descending order using Bubble Sort.
8. Display valid and invalid vote counts.
9. Display candidates and vote totals in descending order.
10. If valid votes are zero, report no winner.
11. Else if more than one candidate has the maximum, report a tie and list tied candidates.
12. Otherwise, report the winner.
13. Stop.

SAMPLE INPUT
Candidates: 4
Votes: 12
1 2 1 3 2 1 4 2 3 0 5 -1

EXPECTED OUTPUT
Valid votes = 9
Invalid votes = 3
Candidate 1 = 3
Candidate 2 = 3
Candidate 3 = 2
Candidate 4 = 1
Election result: TIE
Tied candidates: 1 2

COMPLEXITY
Vote counting: O(n). Candidate sorting: O(c^2). Overall: O(n + c^2).
