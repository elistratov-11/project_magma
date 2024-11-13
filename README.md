#include <stdio.h>
#include <math.h>

int change(int *array, int *new_array){
    int table[8][16] = {
    {12, 4, 6, 2, 10, 5, 11, 9, 14, 8, 13, 7, 0, 3, 15, 1},
    {6, 8, 2, 3, 9, 10, 5, 12, 1, 14, 4, 7, 11, 13, 0, 15},
    {11, 3, 5, 8, 2, 15, 10, 13, 14, 1, 7, 4, 12, 9, 6, 0},
    {12, 8, 2, 1, 13, 4, 15, 6, 7, 0, 10, 5, 3, 14, 9, 11},
    {7, 15, 5, 10, 8, 1, 6, 13, 0, 9, 3, 14, 11, 4, 2, 12},
    {5, 13, 15, 6, 9, 2, 12, 10, 11, 7, 8, 1, 4, 3, 14, 0},
    {8, 14, 2, 5, 6, 9, 1, 12, 15, 4, 11, 0, 13, 10, 3, 7},
    {1, 7, 14, 13, 0, 5, 8, 3, 4, 15, 10, 6, 9, 12, 11, 2}
    };
    for (int i=0; i<8; i++){
        new_array[i] = table[i][array[i]];
    }
    return 0;
}

int out(int *array){
    for (int i=0; i<8; i++){
        printf("%x ", array[i]);
    }
    return 0;
}

unsigned long dec(int *array){
    unsigned long a;
    unsigned long step(int a, int b);
    a = array[0]*step(16, 7)+array[1]*step(16, 6)+array[2]*step(16, 5)+array[3]*step(16, 4)+array[4]*step(16, 3)+array[5]*step(16, 2)+array[6]*16+array[7];
    return a;
}

int hex(int *array, unsigned long numb){
    array[7] = numb%16;
    numb = numb/16;
    array[6] = numb%16;
    numb = numb / 16;
    array[5] = numb % 16;
    numb = numb/16;
    array[4] = numb%16;
    numb = numb/16;
    array[3] = numb%16;
    numb = numb / 16;
    array[2] = numb%16;
    numb = numb / 16;
    array[1] = numb%16;
    numb = numb /16;
    array[0] = numb%16;
    return 0;
}

unsigned long step(int a, int b){
    unsigned long ans=1;
    for (int i=0; i<b; i++){
        ans *= a;
    }
    return ans;
}

int same(int *array, int *new_array){
    for (int i=0; i<8; i++){
        new_array[i] = array[i];
    }
    return 0;
}

int main(){
    int a[8] = {0, 1, 0, 2, 0, 3, 0, 4};
    int b[8] = {0, 5, 0, 6, 0, 7, 0, 8};
    int c[8] = {0xf, 1, 0xf, 2, 0xf, 3, 0xf, 4};
    int d[8] = {0xf, 5, 0xf, 6, 0xf, 7, 0xf, 8};
    int k[8][8] = {{8, 1, 8, 2, 8, 3, 8, 4}, 
            {8, 5, 8, 6, 8, 7, 8, 8},
            {8, 9, 8, 10, 8, 11, 8, 12}, 
     {8, 13, 8, 14, 8, 15, 8, 0},
            {13, 1, 13, 2, 13, 3, 13, 4}, 
     {13, 5, 13, 6, 13, 7, 13, 8},
            {13, 9, 13, 10, 13, 11, 13, 12}, 
     {13, 13, 13, 14, 13, 15, 13, 0}};
    unsigned long numb, key, swap, swap1;
    out(a);
    out(b);
    printf("\n");
    int a1[8];
    unsigned long sum;
    for (int i=0; i<3; i++){
 for (int j=0; j<8; j++){
            numb = dec(a);
            key = dec(k[j]);
     same(a, a1);
            sum = (numb+key)%4294967296;
            hex(a, sum);
            change(a, a);
     swap = dec(a);
     swap1 = swap<<11 | swap>>21;
     hex(a, swap1);
            hex(a, (dec(a)^dec(b))%4294967296);
     same(a1, b);
 }
    }
    for (int i=7; i>=0; i--){
        numb = dec(a);
 key = dec(k[i]);
 same(a, a1);
 sum = (numb+key) % 4294967296;
 hex(a, sum);
 change(a, a);
 swap = dec(a);
 swap1 = swap<<11 | swap1>>21;
 hex(a, swap1);
 hex(a, (dec(a)^dec(b))%4294967296);
 same(a1, b);
    }
    out(a);
    out(b);
    printf("\n");
    return 0;
}
