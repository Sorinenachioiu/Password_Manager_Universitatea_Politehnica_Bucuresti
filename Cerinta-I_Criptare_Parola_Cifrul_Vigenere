#include <fstream>
#include <cstring>

using namespace std;
ifstream in("pwd.in");
ofstream out("pwd.out");

const int DIM = 100;//maximum dimension of the plain pswd


//verify if the key and the plain pswd are valid
bool valid(char str[])
{
    register int i;
    for(i = 0; i < strlen(str); i++)
    {
        if(!((str[i] >= 'a' && str[i] <= 'z')||
             (str[i] >= 'A' && str[i] <= 'Z')))
            return 0;//one char is not a letter
    }
    return 1;//all the elements of str are letters
}

//multiplicate the key in order to be the same lenght as the plain pwd
//the function is passed the key and the dimension of the plain text
void key_multiplication(char str[], int dim)
{
    register int i;
    int init_dim = strlen(str);//init_dim = initial lenght of the key

    for(i = init_dim; i <= dim; i++)
    {
        str[i] = str[i-init_dim];
        str[i+1] = NULL;
    }
}

//calculate distance between the 'a' letter to the one stored in a
int dist_to_a(char a)
{
    if(a >= 'A' && a <= 'Z')
        return a - 'A' + 26;
    return a - 'a';
}

//converts a value to a letter of the alphabet
char to_letter(int dist)
{
    if(dist < 26)
        return dist + 'a';
    return dist - 26 + 'A';
}

//generates one encrypted letter(the encryption of char b with char a of the key)
char new_letter(char a, char b)
{
    int dist;//stores the new value of the current letter

    dist = (dist_to_a(a) + dist_to_a(b)) % 52;
    return to_letter(dist);
}

//encrypt the plain text with the generated key
void encryption(char key[], char str[])
{
    register int i;
    int L = strlen(str);//store the lenght of str
    for(i = 0; i < L ; i++)
    {
        str[i] = new_letter(key[i], str[i]);
    }
}

int main()
{
    char plain[DIM + 3], key[DIM + 3];//declare the key and the plain pswd

    in >> key >> plain;

    if(!valid(key) || !valid(plain))
    {
        out << "INVALID";//the key or the plain pswd are not correct
    }
    else
    {
        key_multiplication(key, strlen(plain));
        encryption(key, plain);
        out << plain;//output the encrypted password
    }
    return 0;
}
