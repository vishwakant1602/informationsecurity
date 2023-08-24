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

