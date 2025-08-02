# Problem 1

```c++
   int i=0,sum = 0;
    while(i<n)
    {
        int j=0;
        while(j<n)
        {
            sum += j;
            j+=2;
        }
        i++;
    }
```
- Solution: As there is a loop inside another means nested loop so it is O(n^n) or quadratic time.

# Problem 2

```c++
 for(int i=0;i<n;i+=10)
    {
        for(int j=n;j>=0;j--)
        {
            cout << "Hello" << endl;
        }
    }
    for(int i=0;i<n;i++)
    {
        cout << "Hi" << endl;
    }

```

- Solution: First two loops are nested loop so it is O(n^n) or quadratic time. The third loop in O(n) or linear time. Worst is quadratic time. So the time complexity is O(n^n).

# Problem 3

```c++
for(int i=0;i<n;i++)
    {
        int j=0;
        while(j*j<n)
        {
            i+j;
            j++;
        }
    }
```

- Solution: The nested loop is running in square-root time and first loop is linear time. So the time complexity is O(n√n).

# Problem 4

```c++
 for(int i=0;i<n;i++)
    {
        for(int j=n;j>=0;j--)
        {
            for(int k=1;k<=n;k++)
            {
                sum += i+j+k;
            }
        }
    }


    for(int i=0;i<n;i++)
    {
        for(int j=1;j<=n;j++)
        {
            sum += i+j;
        }
    }
```

- Solution: In the first part there are three nested loop. So it is O(n^3) or cubic time. In the second part there are two nested loop. So it is O(n^2) or quadratic time. The worst is cubic time. So the time complexity is O(n^3).

# Problem 5

```c++
for(int i=0;i*i<n;i++)
    {
        sum += i;
    }


    for(int i=0;i<n;i++)
    {
        sum += i;
        i*=k;
    }
```

- Solution: Both loop are running in square root time. So the time complexity is O(√n).

# Problem 6

```c++
for(int i=0;i<n;i++)
    {
        cin >> a[i];
    }
    sort(a,a+n);
```

- Solution: First loop is running in linear time. So the time complexity is O(n). sort function using logarithmic time so the time complexity is O(n log n). So the ultimate time complexity is O(n log n).


# Problem 7

```c++
for(int i=0;i<n;i++)
    {
        sort(a,a+n);
    }
```

- Solution: Outer loop is running in linear time. So the time complexity is O(n). The sort function is running in logarithmic time so the time complexity is O(n log n). So the ultimate time complexity is O(n*n log n).
