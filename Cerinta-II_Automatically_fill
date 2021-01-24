#include <cstdlib>
#include <cstring>
#include <iostream>

using namespace std;

const int NMX = 1000;//maximum dimension of a text

struct pereche
{
	char *camp, *valoare;
};

pereche pairs[NMX + 5];//stores the n pairs of autofill informations
char text[NMX + 5], temp[NMX + 5];//text is the field that needs to
                                  //be autofilled
int n, pos;

//read a single field of a pereche
void read(char*& p)
{
    cin >> temp;
    p = (char*)malloc(strlen(temp) + 1);
    strcpy(p, temp);
}

//find the searched field in the sorted pairs
int binary_search(char s[])
{
    int l, r, mid;
    l = 0;
    r = n - 1;
    while (l <= r)
    {
        mid = (l + r) >> 1;
        if (!strcmp(temp, pairs[mid].camp))
            return mid;
        if (strcmp(temp, pairs[mid].camp) < 0)
            r = mid - 1;
        else
            l = mid + 1;
    }
    return -1;
}

//merge two sets of pereche
void merge(pereche v[], int &l, int &r, int &mid)
{
    register int i, j, k;

    int dim_l_mid, dim_mid_r;//dimensions of the two halfs
    dim_l_mid = mid - l + 1;
    dim_mid_r = r - mid;
    pereche Lpairs[dim_l_mid + 2],
            Rpairs[dim_mid_r + 2];//the two vectors
                                  //which will be merged

    //copy the values from the vector in the two halfs
    for(i = 0; i < dim_l_mid; i++)
        Lpairs[i] = v[i + l];
    for(i = 0; i < dim_mid_r; i++)
        Rpairs[i] = v[i + mid + 1];

    //merge the two halfs
    i = j = 0;
    for(k = l; i < dim_l_mid && j < dim_mid_r; k++)
    {
        if (strcmp(Lpairs[i].camp, Rpairs[j].camp) <= 0)
            v[k] = Lpairs[i++];
        else
            v[k] = Rpairs[j++];
    }
    for(;i< dim_l_mid; i++)
        v[k++] = Lpairs[i];
    for(;i< dim_mid_r; i++)
        v[k++] = Lpairs[i];
}

void merge_sort(pereche v[], int l, int r)
{
    if (l < r)
    {
        int mid = l + ((r - l) >> 1);
        merge_sort(v, l, mid);
        merge_sort(v, mid + 1, r);
        merge(v, l, r, mid);
    }
}

int main()
{
    int i, j;
    cin >> n;

    //read the n pairs
    for (i = 0; i < n; ++i)
    {
        read(pairs[i].camp);
        read(pairs[i].valoare);
    }

    //sort lexicographically the n pairs in order to be able to
    //binary search elements
    merge_sort(pairs, 0, n - 1);

    cin.get();
    cin.get(text, NMX);//read the string that will be autofilled

    for (i = 0; i < strlen(text); ++i)
    {

        if(isalpha(text[i]))
        {
            strcpy(temp, "");//make temp an empty string
            while(isalpha(text[i]))
            {
                strncat(temp, &text[i], 1);
                i++;
            }

            i--;

            pos = binary_search(temp);//search the field in pairs

            //check if the field exist in pairs
            if (pos != -1)
                cout << pairs[pos].valoare;//display the value of field
            else
                cout << temp;//display the string that was read

        }
        else
        {
            cout <<text[i];//display anything else than a letter
        }
    }

    return 0;
}
