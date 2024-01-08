## Count Sort:-
### Problem0:-  Find the smallest number that can be formed by rearranging the digits of the given input.   
1.  if we have an array A, in which A[i] (means every element array is the digit) is repersenting the digits.    now digits will be 0 to 9 in numbers.
```
       0 1 2 3 4
    A=[1 3 5 2 3]                   // these are the digits, 
        
        Ques:-  What is the smallest num can be formed by rearranging the digits ?
        Ans :-  1 2 3 3 5           // rearranging like this, we formed the smallest number.
        
        Ques:-  What actually we are doing here ?
        Ans :-  Sorting in Ascending order. 
        
        If we apply merge sort algo, then TC = O(N log(N)). 
        but if every element of the array is a digit, then we can do it in better TC, How ? 
            Whatever the o/p is can we say the o/p will look like:- initially some zero's then some one's, then some two's and so on.
            0........0 1.........1 2...........2 3.....3 .... 9.........9
            if we have the count of zero's, one's, two's and so on. then we can find the ans.
            
            means 'we can easily store the frequency of every element'. we can use map for that, but if we have 10 unique digits than Can't we store it in the array.
            so we create the freq array. 
            F[i] --> freq of ith element. 
              
               0 1 2 3 4 5 6 7 8
            A=[1 3 8 3 2 6 5 3 8]
            
            Step 1:-        (Storing the frequency)
                   0 1 2 3 4 5 6 7 8 9
                F=[0 0 0 0 0 0 0 0 0 0]             initially, frequency of every element is 0.
                
                    simply traverse the array, increase the frequency by 1.
                    for i --> 0 to N-1,
                        F[A[i]] += 1;               whenever we find then increase the frequency of A[i]                    // calculating the frequecy.
                    
                F=[0 1 1 3 0 1 1 0 2 0]             updated values of frequency array.
                
                    TC = O(N)
                    SC = O(Range of elements)   ==>    O(1).        the range of elements is 0 to 9, so it is O(10), which is nothing but constant O(1). 
            
            Step 2:-        (Sorting Part)
                From the frequency array, we have to simply iterate & find the smallest possible number that we can have. so for print the ans we traverse the array. 
                
                for i --> 0 to 9                this is running for range of elements which is 0 to 9.
                {
                    for j --> 1 to F[i]         if frequency of i is 2 then  j loop  will run two times,if frequency of i is 5 then  j loop will run five times.
                        print(i)                
                }
                                
                                // basically frequecy of every element or sum of frequency of every element will be N means j loop will running Sum of frequency of every element that will be total no. of elements 
                                   so j loop will run till N times. 
                                   
                                // basically i loop is running for range times, here range is 0 to 9 so it is running 10 times, 
                                    for every time we are running the frequency array (so j loop is not run for every i, if F[i] is 0 then  we are not printing the element). 
                                
                TC = O(N)       although i loop is running for range of elements (which is very small) & (overall printing) j loop is running at maximum N times (print i is printing one element of the array so at max j loop will print N times).
                                we can print like this TC = O(Range + N)    ==>     O(N)  becoz range is very small.
                SC = O(1)
                
                                j loop is, Sigma Frequency of i, i is going from 0 to 9 that will be 1 + 1 + 3 + 1 + 1 + 2 = 9  {sum of frequency of every element}. 9 is the total elements of the array.
                                    so j loop will gives us the N. img 1. 
            
            Total TC & SC:-
                TC:-    O(N)
                SC:-    O(1)        // This is better than any sorting algorithm done till now, 
        
        The algorithm which we are doing "Storing the frequency & then doing the sorting part" is know as count sort algorithm. 
        if the count sort is that much good algo which has O(N) time complexity & constant space. then why we are doing other sorting algo. 
        
        Scanerio:-
            if A[i] <= 10^9     then count sort algo will not work, 
                becoz 'Storing or Creating the array is large, so we will get Memory Limit Exceed error'.
                    if we use Map (the Sorted Map) then the  insertition part is O(log N) time. means if we insert the frequecy array values in the tree map then TC is O(N log(N)). so no better than normal sorting algo.
                    if we use Map (the Un-Sorted Map) then the data is not stored in the linear fashion, randomly stored. so we have to iterate all the way from smallest to largest number. 
                so for this large data 10^9, count sort is not applicable.
                therefore, this kind of scanerio we use merge sort || quick sort. 
```
#### Problem0:-  if -10 <= A[i] <= 10
```    0  1   2 3 4 5  6  7  8
    A=[3 -8 -10 3 0 10 2 -6 -8]
    
        The Range of data from [-10 to 10].
        Ques:-  From the above range, How many data we will have ?
        Ans :-  21.
            
        Frequency Array of size 21:-
           indexing             0   1   2   3   4   5   6   7   8   9   10  11 12 13 14 15 16 17 18 19 20        these indexing will not store the frequency of 0, 1, ..... || 14, ......  20 and so on. becoz we don't have elements 14, 20, 11, 9 and so on.
                                                                                                                 we want to store the frequecy of -10 to 10.
                               -10 -9  -8  -7  -6  -5  -4  -3  -2  -1   0    1  2  3  4  5  6  7  8  9 10        this is the range of our data -10 to 10.
                               
           Ques:-   Now, What is F[i] ? 
           Ans :-   frequency of i-10. it can also be written as (i + min_element)
                    ex:-    if i=0, then i - 10             ||      (i + min)       -10 is the minimum element. 
                                         0 - 10 = -10                0 + -10
                    so at index 0, we are storing the frequency of -10.                      
                                         
                    ex:-    if i=3, then i - 10             ||      (i + min)       -7 is the minimum element. 
                                         3 - 10 = -7                0 + -7
                    so at index 3, we are storing the frequency of -7.                      
        
        Code:-
                iterate the complete array from left to right,
                while iterating the complete array, frequency of A[i]+10             (assume A[i]=3 then index 13 will get change)  
                    like:-
                        i=0 A[i]=3,       3+10= 13        so at index 13, we will update the frequency count of element  3.         count=1
                        i=1 A[i]=-8,     -8+10=  2        so at index  2, we will update the frequency count of element -8.         count=1
                        i=2 A[i]=-10,   -10+10=  0        so at index  0, we will update the frequency count of element -10.        count=1
                        i=3 A[i]=  3,    3+10= 13        so at index 13, we will update the frequency count of element    3.        count=2
                        i=4 A[i]=  0,    0+10= 10        so at index 10, we will update the frequency count of element    0.        count=1
                        i=5 A[i]= 10,   10+10= 20        so at index 10, we will update the frequency count of element   20.        count=1
                        and so on. 
                
                for i --> 0 to (N-1)
                    F[A[i]+10] += 1;    
        
                    there are tiny change in frequency part.
                Dry Run:-                                                          Index
                        first element is 3, so we increase the frequency of 3+10=   13  by 1. count=1
                        next element is -8, so we increase the frequency of -8+10=  2  by 1. count=1
                        next element is -10, so we increase the frequency of -10+10=0 by 1. count=1
                        next element is 3, so we increase the frequency of 3+10=    13  by 1. count=2
                        next element is 0, so we increase the frequency of 0+10=    10  by 1. count=1
                        next element is 10, so we increase the frequency of 10+10=  20  by 1. count=1
                        next element is 2, so we increase the frequency of 2+10=    12  by 1. count=1
                        next element is -6, so we increase the frequency of -6+10=  4  by 1. count=1
                        next element is -8, so we increase the frequency of -8+10=  2  by 1. count=2
                        everything else will be 0. 
                
                   
                TC = O(N)
                SC = O(Range) ==> O(21) = O(1). 
                
                Once we have the frequency array, From this frequency array, we have to print the sorted order.     ||  we can also update the input array becoz we already stored it. so we re-write the values in input array.     ||     we directly print the ans 
                but one Small Change will be there,
                    :-  If we travelling the entire range of the data, img 2.  
                            for i --> -10 to 10.            so travelling the entire range.
                                for j --> 1 to F[i+10]      now frequency of i will not be at index i, it is at i+10.       like i=-10, so -10 will be at index 0, we can found it via i+10  ||  -10+10=0.  therefore F[i+10]=1 so we print i, 1 times, becoz count of -10 is 1.
                                    print(i).               img 3.
                the changes will be img 4. (highlighted area)
                
                TC = O(N)       first loop is running 20 times, second loop is running till Frequency array so it is linear time.      
                SC = O(1). 

        So, count sort is very very helpful if we the range of elements is small. 
        
        Conclusion:-
                "We can apply Count Sort on Negative numbers as well".
                                                
```
### If any number is given & we want to know the unit digit of that number.
``` 
      210          digits positions like 0 digit called unit digits, ones digit & two digit.
    N=368
      we simply do N%10 & we get the ans.  img 4.
    
    Ques:-  How to find the tens digit of the number ?              N=368, 8 are located at ones/units place,  6 are located at tens place,  3 are located at huendereds place.
    Ans :-  
            we have N=368,
            when we do N/10     ||  368/10 = 36.  now it becomes 36.       basically unit digis has gone.
            now we do (N/10)%10 ||  36%10 = 6
            
    Ques:-  How to find the huendereds digit of the number ?              
    Ans :-  
            we have N=368,
            when we do N/100     ||  368/100 = 3.  now it becomes 3.      
            now we do (N/100)%10 ||  3%10 = 3
             
    Observation:-
        "to find the i'th digit the formula is (N/10^i)%10", this is how we can find the i'th digit of any N. 
        like:-
            if i=0 then we find unit digit.
            if i=1 then we find tens digit.
            if i=2 then we find hunderds digit.
            ... and so on.
```
###  How to use Inbuilt sorting functions.  
``` 
    In java, Collection.sort() fun is available.
        if normal integer array is given then we pass the array to the sort() & it's sort in ascending order.
        but If we want to sort in particular order.
            like:-  
                    based on no. of factors we will sort.
                    based on no. of digits we will sort.
                    based on no. of descending order we will sort.
                    ... and so on.
        for that we will use Comparator, 
        Comparator:-    logical mean.
                let say Kartik is an program/compiler & mayur is writing a code so that kartik will run that code. kartik is telling that 'I know only ascending order', if mayur will give only input array then kartik will sort in ascending order.
                but if mayur wants kartik to sort in mayur choice then "tell kartik that, how to compare the data (how compare two things)" then kartik can sort the data according to mayur choice. 
                So, What Comparator say's, Comparator has function called Compare function.  usually the return type is int. In Compare fun we have two objects A, B.  & We have to tell the program that how to compare A & B, (means write a compare fun, to compare the data)
                   {two objects means, if we have integer arrayn then A & B will be integers, if we have char arrayn then A & B will be chars and so on}    compare fun just wants to know how to compare these two things.
                   In Compare fun we will write three things,
                        {
                        return Negative numbers -->  means when we return the negative number then we tell the program 'among these two elements A is actually smaller than B'
                        return zero  -->  means when we return the zero then we tell the program 'these two elements are equal'.
                        return Positive numbers -->  means when we return the Positive number then we tell the program 'among these two elements A is actually greater than B'
                        }
                      this is the way of telling the compare function that which element/object are greater object.
                   now program will know how to compare the data. like which data should be treated as small data or large data. 
                   this is one way of we are telling the program, this is how the comparision work. & return the data accrodingly.  that's how comparator works. 
                img 5.
```
### Sort the integer array, with respect to k th digit of the number. (based on Comparator)
```
    A=[326, 18, 523]        k=0.    means we want to sort the data with respect to the unit digits.
        
        326     18    523.
          6      8      3   are the unit digits of the number.
        523     326   18    after sorting, with respect to unit digits if we sort the data, then the data will look like 

    A=[362, 399, 318]       k=2     means we are looking for a 'hundereds digit of the number' || 'third place of any number' based on thas we want to sort the data.
        according to hundereds digit of the number, all the number equal. 362, 399, 318.
        now we have to maintain the stability. so the o/p is,
        362, 399, 318.
    
    so, given the k th digit we have to sort the input array.    
        
    How ?
        for doing this, we can use comparator (means inbuilt sorting algo)& sort the data. basically we will pass two numbers (in compare function) & we find out the kth digit (img 6). with respect to k th digit we return the value. so we can use the inbuilt sorting function. 
        but TC of inbuilt sorting is N log N.
    
    if we don't want to use comparator, inbuilt sorting algo, compare function etc. then, 
         
         A=[361, 432, 12, 78, 500, 112]     k=1     means we are looking at the tens digit of a number.
            12  &   112 both the number are equal so we have to maintain the stability.
            it is similar as the first question (sorting digits). but the difference is, here we don't have the digit to sort.
                means we have this array is given & we have to store the F[1] is 2  (means there are two numbers in the array which have 1 at the tens location).
                but, if we give this F[1]=2 then Can we generate 12, 112 number (means if we only know the frequency of the tens digit). 
                    Not possible.
                so instead of 'creating frequency array (which can store the count{of digit}), we should "create frequency array of a list" (means every element is a list)'
                F[i] --> list of elements where k th digit is i.
                    we have array of size 10 (img 7). & one element of the array is list. so it's like 2d array || array of list || list of list.
                we will iterate the array & we add the elements into list, based on the k th digit. wherever there are no elements then there are empty list.
                    img 8. this is how we calculate the frequency list.     
                    & whe we store the element then we maintain the stability.  so it will keep track of order in which data is present. 
                now, we have to iterate every list & print the element. where list is empty then nothing to do. 
            
            500 12 112 432 361 78, based on tens digit, we sort the data.       ==>     it is kind of Count Sort but the every element is list.
            
            Total:-
                The sum of length of every list is:-  every element will be part of only one list. so the total sum of length will be O(N).          (means we are travelling every list)
                so, even if we travel every list then TC is:- O(N).     so total TC is linear, (from the array to generate the frequency list, it will take line TC like we travel the array, {same as count sort} insert in the list). travel every list & get the ans.  
                                                      SC is:- O(N). 
    This is the base of Radix Sort.        
``` 
### Radix Sort
1.  Radix Sort basically says, **Sort Digit by Digit**
``` 
    A=[361, 432, 12, 78, 500, 112]     
        this algo says, Take all the number & try to sort them digit by digit. 
        it means, number written like this (img 9). if we only pick up the units digit, so we can apply the above algo using the K=0 scanerio. 
            finaly array look like (img 10). we are maintaing the stability like 432 12 are follow the order in which they are arranged.
        numbers which we arranged in (img 10) using k=0, 
        now if there a decision made that we need to arrange the number based on tens digit (img 11). then Can the decision over power the unit digits ? 
            like:-
                there are two numbers, 38 42.
                now the unit digit tells us that 8 is larger than 2. but tens digit is saying that 3 is smaller than 4.
                What we will say, 38 is smaller || 42 is smaller.
                    38 < 42     (basic maths)
                Disclamer by Me:-
                     first we sort the number based on units digit there 8 is larger than 2, so the o/p should be 42 38 this would be the order.
                     but second we sort the number based on tens digit there 3 is smaller than 4, so the o/p should be 38 42 this would be the order. here, tens digit dominate the ans of unit digit. 
        We can say that the weight of units digit is less than tens digit.  means whatever the tens digit say than will dominate units digit.       ********************Imp*****************************
        so, first we made the decision based on units digit (img 10) k=0, now we will make the decision based on tens digit k=1.
        'If there is a Change in the order we can do, but the reverse we can't do', means if we want to sort the data based on tens digit & later on we sort the data based on units digit.
        the Units digit are not that much powerfull to change the order of elements descided by tens digit. (tens digit will dominate the unit digits).
        now the order k=2 look like, (img 13) for the places where the hundereds digit is not there that will be 0.
        so, based on the hundereds digit if there is any change that will be dominating the other (unit, tens) changes. 
            like:-  
                    if hundereds digit tells that 500 is biggger than 012 then it is right.
        sorted order.   (if we have large number then we can add more digits & sort the data).
        so digit by digit we apply the radix sort.
               
    TC = O(N * No. of digits)
    SC = O(N)       // becoz we are using the frequency arraylist. 
```
### TC = O(N * No. of digits)   this TC we have not seen in past. so doing Analytics. 
``` 
    Ques:-  What is the Size of the array in programming language ? 
    Ans :-  N=10^5
    
        Ques:-  What is N * No. of digits ? 
        Ques:-  What is no. of digit in this case ? 
        Ans :-  

    Ques:-  What is the Range of integer array in programming language ? 
    Ans :-  A[i]<=10^9

    rewatch this Analytics part. 
    
    Conclusion:-
            "with respect to TC Merge Sort, Quick Sort & Radix Sort are same".
            
            "Inbuilt Sorting function do not use Radix Sort".
                Reasons:-
                    1.  Whenever we have inbuilt sorting algorithm sometimes we want to sort the data in randomised order, so if we use Radix sort as inbuilt function than it will not able to handle it.
                            becoz Radix sort do not compare the objects directly || it do not compare the two elements directly, means there is No Comparision Parameters. 
                            so it's not the comparision algorithm.  we can't write custom comparator.  
                    2.  When we create any inbuilt function that will be used world wide than we make sure that it is suitable for majority scanerios. 
                            so if we pass the array that will be of any type like array of int, array of char and so on. at the end it will give the sorted array.
                            means any data type will give us perfect sorted array in the output.  
                            
                            Radix sort may not work || take lot of space || take lot of space:-
                                if we pass string that has also limits. 
                                if we pass the floating point that has no limits. 
                                    double. 
                                        see in pdf, here we are actually travelling the digit so the digit by digit comparision can go very high. we are not travelling 4 digits like 3112, we are travelling till decimal like 3112.368256. 
                                        so the TC will increase, that's why it is advisible that do not use Radix Sort in inbuilf function, so we use Merge || Quick Sort are the best sorting algo in inbuilt function.
```
