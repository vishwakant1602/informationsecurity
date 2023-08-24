# informationsecurity
#ceaser
#include<bits/stdc++.h>
using namespace std;
string decryption(int key,string cipherText){
    string plainText = "";
    key = 26 - key;
    for(int i=0;i<cipherText.size();i++){
        if(cipherText[i]!=' '){
            if(islower(cipherText[i])){
                int index = cipherText[i]-'a';
                char a = (index+key)%26 + 97;
                plainText+=a;
            }
            else{
                int index = cipherText[i]-'A';
                char a = (index+key)%26 + 65;
                plainText+=a;
            }
        }
    }
    return plainText;
}
string encryption(int key,string plainText){
    string cipherText = "";
    for(int i=0;i<plainText.size();i++){
        if(plainText[i]!=' '){
            if(islower(plainText[i])){
                int index = plainText[i]-'a';
                char a = (index+key)%26 + 97;
                cipherText+=a;
            }
            else{
                int index = plainText[i]-'A';
                char a = (index+key)%26 + 65;
                cipherText+=a;
            }
        }
    }
    return cipherText;
}
int main(){
    int key;
    cout<<"Enter key: ";
    cin>>key;
    string message;
    cout<<"Enter message to encrypt: ";
    cin>>message;
    string cipherText = encryption(key,message);
    string plainText = decryption(key,cipherText);
    cout<<cipherText<<endl;
    cout<<plainText<<endl;
    return 0;
}

#mono
#include<bits/stdc++.h>
using namespace std;
unordered_map<char, char> generateMappingTable1() {
    unordered_map<char, char> mappingTable;
    string sourceChars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
    string targetChars = "xM8kABGwT6pqSZJcd9frDVL0NEm2zOHYRQa5jbKFuU3o74iegnh1WtXlvsICP";

    for (int i = 0; i < sourceChars.size(); ++i) {
        mappingTable[sourceChars[i]] = targetChars[i];
    }

    return mappingTable;
}
unordered_map<char, char> generateMappingTable2() {
    unordered_map<char, char> mappingTable;
    string sourceChars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
    string targetChars = "xM8kABGwT6pqSZJcd9frDVL0NEm2zOHYRQa5jbKFuU3o74iegnh1WtXlvsICP";

    for (int i = 0; i < sourceChars.size(); ++i) {
        mappingTable[targetChars[i]] = sourceChars[i];
    }

    return mappingTable;
}
string encryption(string Text){
    string changeText;
    unordered_map<char,char> map = generateMappingTable1();
    for(int i=0;i<Text.size();i++){
        changeText+=map[Text[i]];
    }
    return changeText;
}
string decryption(string Text){
    string changeText;
    unordered_map<char,char> map = generateMappingTable2();
    for(int i=0;i<Text.size();i++){
        changeText+=map[Text[i]];
    }
    return changeText;
}
int main(){
    string message;
    cout<<"Enter message: ";
    cin>>message;
    string cipherText = encryption(message);
    string plainText = decryption(cipherText);
    cout<<cipherText<<endl;
    cout<<plainText<<endl;
    return 0;
}


#polualphabetic
#include<bits/stdc++.h>
using namespace std;
unordered_map<char, char> generateMappingTable1() {
    unordered_map<char, char> mappingTable;
    string sourceChars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
    string targetChars = "xM8kABGwT6pqSZJcd9frDVL0NEm2zOHYRQa5jbKFuU3o74iegnh1WtXlvsICP";

    for (int i = 0; i < sourceChars.size(); ++i) {
        mappingTable[sourceChars[i]] = targetChars[i];
    }

    return mappingTable;
}
unordered_map<char, char> generateMappingTable2() {
    unordered_map<char, char> mappingTable;
    string sourceChars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
    string targetChars = "xM8kABGwT6pqSZJcd9frDVL0NEm2zOHYRQa5jbKFuU3o74iegnh1WtXlvsICP";

    for (int i = 0; i < sourceChars.size(); ++i) {
        mappingTable[targetChars[i]] = sourceChars[i];
    }

    return mappingTable;
}
string encryption(string Text){
    string changeText;
    unordered_map<char,char> map = generateMappingTable1();
    for(int i=0;i<Text.size();i++){
        changeText+=map[Text[i]];
    }
    return changeText;
}
string decryption(string Text){
    string changeText;
    unordered_map<char,char> map = generateMappingTable2();
    for(int i=0;i<Text.size();i++){
        changeText+=map[Text[i]];
    }
    return changeText;
}
int main(){
    string message;
    cout<<"Enter message: ";
    cin>>message;
    string cipherText = encryption(message);
    string plainText = decryption(cipherText);
    cout<<cipherText<<endl;
    cout<<plainText<<endl;
    return 0;
}

#columnar
#include <bits/stdc++.h>
using namespace std;
string decryption(int key,vector<vector<char>> map){
    string plainText = "";
    for(int i=0;i<map.size();i++){
        for(int j=0;j<map[0].size();j++){
            if(map[i][j]=='-'){break;}
            plainText+=map[i][j];
        }
    }
    
    return plainText;
}
string encryption(int key,string plainText){
    int row = plainText.size()/key;
    if(plainText.size()%key!=0){
        row+=1;
    }
    int col = key;
    vector<vector<char>> map(row,vector<char>(col,'-'));
    int x = 0;
    int y = 0;
    string chipherText="";
    for(int i=0;i<plainText.size();i++){
        map[y][x] = plainText[i];
        x++;
        if(x >= col){
            y++;
            x=0;
        }
    }
    for(int i=0;i<map.size();i++){
        for(int j=0;j<map[0].size();j++){
            cout<<map[i][j]<<" ";
        }
        cout<<endl;
    }
    for(int i=0;i<map[0].size();i++){
        for(int j=0;j<map.size();j++){
            if(map[j][i]!='-')
            chipherText+=map[j][i];
        }
    }
    cout<<decryption(key,map)<<" ";
    return chipherText; 
}
int main(){
    string plainText = "";
    cout<<"Enter plain text: ";
    cin>>plainText;
    int key;
    cout<<"Enter Key value: ";
    cin>>key;

    cout<<encryption(key,plainText)<<" ";
    return 0;
}

#hillcipher
#include<bits/stdc++.h>
using namespace std;
string encryption(vector<vector<int>> key,string plainText){
    vector<int> arr; 
    for(int i=0;i<plainText.size();i++){
        int a = islower(plainText[i]) ? plainText[i] - 'a' : plainText[i] - 'A';
        arr.push_back(a);
    }
    int x = 0;
    int y = 0;
    while(x < arr.size()){
        for(int i=0;i<key.size();i++){
            int a = 0;
            for(int j=0;j<key[0].size();j++){
                a+=(key[i][j]*arr[x])%26;
                x++;
            }
            arr[y] = a;
            y++;
        }
    }
    for(auto i:arr){
        cout<<i<<" ";
    }
    return "";
}
int main(){
    // Implement 2*2 matrix key
    // let key matrix 2*2
    vector<vector<int>> key;
    key.push_back({6,24});
    key.push_back({13,16});
    
    string message;
    cout<<"Enter message: ";
    cin>>message;
      
    int cnt = message.size()%key.size();

    for(int i=0;i<cnt;i++){
        message+='a';
    }
    cout<<encryption(key,message);
    return 0;
}

#updated polyalphabetic
#include<bits/stdc++.h>
using namespace std;
string decryption(string cipherText,string keyword){
   string plainText;
    for(int i=0;i<cipherText.size();i++){
        int step = islower(keyword[i]) ? keyword[i] - 'a' : keyword[i] - 'A';
        step = 26 - step;
        if(cipherText[i]!=' '){
            if(islower(cipherText[i])){
                int index = cipherText[i]-'a';
                char a = (index+step)%26 + 97;
                plainText+=a;
            }
            else{
                int index = cipherText[i]-'A';
                char a = (index+step)%26 + 65;
                plainText+=a;
            }
        }
        else{
            plainText+=cipherText[i];
        }
    }

    return plainText;
}
string encryption(string plainText,string keyword){

    string cipherText;
    for(int i=0;i<plainText.size();i++){
        int step = islower(keyword[i]) ? keyword[i] - 'a' : keyword[i] - 'A';
        if(plainText[i]!=' '){
            if(islower(plainText[i])){
                int index = plainText[i]-'a';
                char a = (index+step)%26 + 97;
                cipherText+=a;
            }
            else{
                int index = plainText[i]-'A';
                char a = (index+step)%26 + 65;
                cipherText+=a;
            }
        }
        else{
            cipherText+=plainText[i];
        }
    }

    return cipherText;
}
int main(){
    string message;
    cout<<"Enter a message: ";
    cin>>message;
    string keyword;
    cout<<"Enter keyword in form of string: ";
    cin>>keyword;
    keyword = keyword + message;
    string cipherText = encryption(message,keyword);
    cout<<cipherText<<endl;
    cout<<decryption(cipherText,keyword)<<endl;
    return 0;
}

#playfair
#include<stdio.h>
#include<strings.h>
#include<string.h>

void choice_fill();
char encryption(char []);
void decryption(char []);
void play_fair();

char key[100],play[5][5],ct[255],msg[255],plain_text[255],c_text[255];

void main(){
    int i,choice,flag=0,j,k,size;
    printf("\n ---play Fair Cipher ---\n");
    printf("Enter plain text : ");
    scanf("%[^\n]",msg);
    size = strlen(msg);
    int count = 0;

    for(i =0; msg[i]; i++){
        if(msg[i] != ' ')
            msg[count++] = msg[i];
        msg[count] = '\0';
    }
    for(i =0; i<size; i=+2){
        if(msg[i]==msg[i+1]){
            for(j = size;j>i;j--){
                msg[j]=msg[size-1];
                size--;
            }
            msg[j+1]='x';
        }
    }
    size = strlen(msg);
    if(size%2 !=0){
        msg[size] = 'x';
        msg[size+1]='\0';
    }
    printf("\n plain text after space remove : %s", msg);
    printf("\n message for encryption is : ");
    for(i =0,j=0; msg[i];i++){
        putchar(msg[i]);
        if(i%2!=0){
            printf(" ");
        }
    }
    choice_fill();
}


void choice_fill(){
    int choice, flag = 0;
    do{
        printf("\n press 1 for encryption \n press 2 for decryption \n press '0' for exit \n ");
        scanf("%d", &choice);
        switch (choice)
        {
        case 1:
            encryption(msg);
            flag=1;
            break;
        case 2:
            if(flag==1)
                decryption(ct);
            else
                printf("first perform encryption process");
            break;
        case 0:
            exit(1);
            break;
        default:
            printf("\n please enter valid choice \n");
            break;
        }
    }while(choice != 0);
}

char encryption(char pt[]){
    int i,j,k,l,r1,r2,c1,c2,p,q;
    printf("\n Plain text : %s", pt);
    play_fair();
    j=1;

    for(i=0; i<strlen(pt);){
        r1=0;r2=0;c1=0;c2=0;p=0;q=0;
        p=pt[i];
        q=pt[j];
        printf("\t");
        putchar(pt[i]);
        putchar(pt[j]);
        printf("=");

        // if(p=='j'){
        //     pt[i]='i';
        // }
        // if(q=='j'){
        //     pt[i]='i';
        // }
        // for(k=0;k<5;k++){
        //     for(l=0;l<5;l++){
        //         if(play[k][l]==p){
        //             r1=k;c1=l;
        //         }
        //         if(play[k][l] == q){
        //             r2=k;c2=l;
        //         }
        //     }
        // }

        if(p=='j'){
            pt[i]='i';
        }
        if(q=='j'){
            pt[i]='i';
        }

        for(k=0;k<5;k++){
            for(l=0;l<5;l++){
                if(play[k][l]==p){
                    r1=k;c1=l;
                }
                if(play[k][l]==q){
                    r2=k;c2=l;
                }
            }
        }

        if(r1==r2){
            ct[i]=play[r1][(c1+1)%5];
            ct[j]=play[r2][(c2+1)%5];
            putchar(ct[i]);
            putchar(ct[j]);
        }
        else if(c1 == c2){
            ct[i]=play[(r1+1)%5][c1];
            ct[j]=play[(r2+1)%5][c2];
            putchar(ct[i]);
            putchar(ct[j]);
             }
        else{
            ct[i]=play[r1][c2];
            ct[j]=play[r2][c1];
            putchar(ct[i]);
            putchar(ct[j]);
        }
        i=i+2;
        j=j+2;
    }
    printf("\n\n \tEncrypted msg is : %s\n", ct);
    return ct;
}

void decryption(char pt[]){
    int i,j,k,l,r1,r2,c1,c2,p,q;
    printf("\n Plain text : %s", pt);
    j=1;

    for(i=0; i<strlen(pt);){
        r1=0;r2=0;c1=0;c2=0;p=0;q=0;
        p=pt[i];
        q=pt[j];
        printf("\t");
        putchar(pt[i]);
        putchar(pt[j]);
        printf("=");

        if(p=='j'){
            pt[i]='i';
        }
        if(q=='j'){
            pt[i]='i';
        }

        for(k=0;k<5;k++){
            for(l=0;l<5;l++){
                if(play[k][l]==p){
                    r2=k;c2=l;
                }
            }
        }

        if(r1==r2){
            ct[i]=play[r1][(c1-1)%5];
            ct[j]=play[r2][(c2-1)%5];
            putchar(ct[i]);
            putchar(ct[j]);
        }
        else if(c1 == c2){
            ct[i]=play[(r1-1)%5][c1];
            ct[j]=play[(r2-1)%5][c2];
            putchar(ct[i]);
            putchar(ct[j]);
             }
        else{
            ct[i]=play[r1][c2];
            ct[j]=play[r2][c1];
            putchar(ct[i]);
            putchar(ct[j]);
        }
        i=i+2;
        j=j+2;
    }
    printf("\n\n \tPlain text msg is : %s\n", ct);

}

//playfair
void play_fair(){
    int i,j,k,size;
    printf("\n enter key : ");
    scanf("%s",key);
    strcat(key,"abcdefghijklmnopqrstuvwxyz");
    size = strlen(key);
    for(i=0;i<size;i++){
        if(key[i]=='j'){
            key[i]=='i';
        }
        for(j=i+1;j<size;){
            if(key[j] == key[i]){
                for(k=j;k<size;k++){
                    key[k]= key[k+1];
                }
                size--;
            }
            else {
                j++;
            }
        }

        for(i=0,k=0;i<5;i++){
            for(j=0;j<5;j++){
                play[i][j] = key[k];
                k++;
            }
            for(i=0;i<5;i++){
                for(j=0;j<5;j++){
                    printf(" ");
                    putchar(play[i][j]);
                }
                printf("\n");
            }
        }
    }

}



