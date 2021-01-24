#include <fstream>
#include <ctime>
#include <cstdlib>
#include <cstring>

using namespace std;
ifstream in("pwd.in");
ofstream out("pwd.out");

typedef char *(*functii) (char &ch);//define a pointer to a function

const int Nmax = 1001;//define the maximum dimension of a password

//random caracter generator between 32 and 125
char gen_car()
{
    int val = rand()%(125-32+1) +32;
    return val;
}

//random string generator of dimension dim
void gen_aleat(char a[], int dim)
{
    int i ;
    for(i = 0; i < dim; i++)
    {
        a[i] = gen_car();
    }
    a[i]=NULL;
}

//first type of encoding
char *codif_1(char &ch)
{
    char *ras;
    int fr[95];//static vector of frequency
               //to memorize the number of appearances of a character
               //not to waste memory , fr[0] represents the number of
               //apparences of the 32th char and fr[94]
               //represents the number of apparences of the 125th char
    for(int i = 0 ; i< 95 ; i++)//vector initialization
    {
        fr[i] = 0;
    }
    char *p = &ch;//p is a pointer to ch's adrress

    while((char)*p>=32 && (char)*p <=125)
    {
        //go through the elements that are in the left of the
        //ch caracter in the vector
        int val = (char)*p;//copy the ASCII code of the char in val
        val -= 32;
        fr[val]++;//increase the frequency of the current character
        p--;//pass to the element situated before the current one
    }

    int val = ch;//val becomes the ASCII code of ch
    val -= 32;
    val = fr[val] + 48 - 1;//val becomes the number of apparences of ch
                           //- 1,his own apparence,
                           //+ 48, the ASCII value of character '0'
    char b = (char) val;
    ras = &b;
    return ras;
}


//second type of encoding
char *codif_2(char &ch)
{
    char *ras;
    int val;
    //interchange the 3rd bit with the 6th one
    if(ch & (1<<6))//if the 6th bit is 1
    {
        if(!(ch&(1<<3)))//if the 3rd bit is 0
        {
            //interchange the values
            val = ch;
            val = val&(~(1<<6));//the 6th bit becomes 0
            val = val^((1<<3));//the 3rd bit becomes 1
        }
    }
    else
    {
        if(ch & (1<<3))//if the 3rd bit is 1
        {
            val = ch;
            val = val^((1<<6));//the 6th bit becomes 1
            val = val&(~(1<<3));//the 3rd bit becomes 0
        }
    }

    //count the number of 1 bits in val
    int cop = val, no_bits = 0;
    while(cop)
    {
        if(cop&1)
        no_bits++;
        cop = cop>>1;
    }

    // aplly OR on val with the 00100000 mask
    val = val | 1<<5;

    //LSB becomes 0 if it was 1
    if(val&1)
        val--;


    ch = val;//ch becomes the character resulted after the 3 operations

    char b = no_bits + 48;//b becomes the no of 1 bits

    ras = &b;
    return ras;
}

//third type of encoding
char *codif_3(char &ch)
{
    char *ras;
    char b = toupper(ch);//we apply toupper to ch and store it in b
    ras = &b;
    return ras;
}

//duplicate the letter on the position poz of a string
void sorinian_duplication(char a[], int poz, int &dim)
{
    a[dim] = 'a';
    dim++;
    a[dim] = NULL;

    int i;
    for(i = dim-1 ; i > poz; i--)
    {
        a[i] = a[i-1];
    }
}

//initial string transformation
void transform(functii fct[], char a[], int dim)
{
    int i;
    for(i = 0; i < dim; i++)//go through the whole string
    {
        int val = rand() % 3;//choose a random number that represents
                             //which encoding to apply to the current
                             //char
        char *ch = fct[val](a[i]);//in ch is stored the ch resulted  
                                  //after applying the
                                  //encoding
        if(val < 2)
        {
            sorinian_duplication(a, i , dim);//duplicate the ith char
            if(val == 0)
            {
                a[i+1] = *ch;//the first type of encoding need the
                             //newly obtained ch after the current
                             //character
            }
            else
            {
                a[i] = *ch;//the second type of encoding need the
                           //newly obtained ch before the current
                           //character
            }
            i++;//we increase i in order to skip the newly added char
        }
        else
        {
            a[i] = *ch;//the third operation only replace the old ch
                       //with the newly obtained one
        }

    }
}

int main()
{
    int seed, dim = 4;
    //read seed
    in >> seed;
    srand(seed);

    //read the dimension of the string that will be generated
    in >> dim;

    char a[Nmax];

    gen_aleat(a, dim);//generate aleatory string

    out<<a<<'\n';//display the initial string

    functii functions[] =
    {
        codif_1,
        codif_2,
        codif_3
    };//create the vector of pointers to functions

    transform(functions, a, dim);//transform the string

    out<<a;//display the string after the transformation

    return 0;
}
