// The code can be seem by pressing "raw" and "history"
#include <iostream>
#include <unistd.h>
#include <cstdlib>
using namespace std;

int main(){

int width;
int height;
cout << "How tall is the map?" << endl;
cin >> height;
cout << "How wide?" << endl;
cin >> width;
int map [height][width];
for (int i = 0; i < height; i++){
        for (int j = 0; j < width; j++){
                map [i][j] = 0;
        }
}
int chance;
int deathTime;
int numsick;
int numppl;
cout << "How many days until the person dies once getting the disease?" << endl;
cin >> deathTime;
cout << "How many people will be in this?" << endl;
cin >> numppl;
cout << "How many people will start out sick?" << endl;
cin >> numsick;
cout << "One in how many people will get sick?" << endl;
cin >> chance;
for (int i = 0; i < numppl; i++){
        int a = 0;
        while (a == 0){
                int x = rand() % height;
                int y = rand() % width;
                if (map [x][y] == 0){
                        if (i < numsick){
                                map [x][y] = deathTime - 1;
                        }
                        else {
                                map [x][y] = deathTime;
                        }
                        a = 1;
                }
                else {
                        a = 0;
                }
        }
}
cout << "*** Day 1 ***" << endl << endl << endl;
for (int i = 0; i < height; i++){
        for (int j = 0; j < width; j++){
                if (map[i][j] == 0){
                        cout << "()";
                }
                else {
                        if (map[i][j] < 10){
                                cout << "0";
                        }
                        cout << map[i][j];
                }
        }
        cout << endl;
}
int a = 1;
int c;
int total;
int d = 1;
int temp;
int ch;
while (a == 1){
        c = 0;
        total = 0;
        d++;
        cout << "*** Day " << d << " ***" << endl << endl << endl;
        cout << "Sick people get one less day to live..." << endl;
        for (int i = 0; i < height; i++){
                for (int j = 0; j < height; j++){
                        if (map[i][j] > 0 && map[i][j] < deathTime){
                                map[i][j]--;
                        }
                        if (map[i][j]==deathTime && ((map[i][j+1]>0 && map[i][j+1]<deathTime) || (map[i][j-1]>0 && map[i][j-1]<deathTime) || (map[i+1][j]>0 && map[i+1][j]<deathTime) || (map[i-1][j]>0 && map[i-1][j]<deathTime))){
                                ch = rand() % chance;
                                if (ch == 1){
                                        map[i][j]--;
                                }
                        }
                }
        }
        for (int i = 0; i < height; i++){
                for (int j = 0; j < width; j++){
                        if (map[i][j] == 0){
                                cout << "()";
                        }
                        else {
                                if (map[i][j] < 10){
                                        cout << "0";
                                }
                                cout << map[i][j];
                        }
                }
                cout << endl;
        }
        cout << endl << endl;
        for (int i = 0; i < height; i++){
                for (int j = 0; j < width; j++){
                        if (map[i][j] > 0){
                                int x = rand() % 11;
                                int y = rand() % 11;
                                temp = map[i][j];
                                if (i+x-5 > 0 && j+y-5 > 0 && i+x-5 < height && j+y-5 < width && map[i+x-5][j+y-5] == 0){
                                        map[i][j] = map[i+x-5][j+y-5];
                                        map[i+x-5][j+y-5] = temp;
                                }
                                if (i+x-5 < 0 && j+y-5 > 0 && j+y-5 < width && map[0][j+y-5] == 0){
                                        map[i][j] = map[0][j+y-5];
                                        map[0][j+y-5] = temp;
                                }
                                if (i+x-5 > 0 && j+y-5 < 0 && i+x-5 < height && map[i+x-5][0] == 0){
                                        map[i][j] = map[i+x-5][0];
                                        map[i+x-5][0] = temp;
                                }
                                if (i+x-5 < 0 && j+y-5 < 0 && map[0][0] == 0){
                                        map[i][j] = map[0][0];
                                        map[0][0] = temp;
                                }
                        }
                }
        }
        cout << "Every person moves..." << endl;
        for (int i = 0; i < height; i++){
                for (int j = 0; j < width; j++){
                        if (map[i][j] == 0){
                                cout << "()";
                        }
                        else {
                                if (map[i][j] < 10){
                                        cout << "0";
                                }
                                cout << map[i][j];
                                c++;
                                total += map[i][j];
                        }
                }
                cout << endl;
        }
        if (c == 0 || total/c == deathTime){
                if (c == 0){
                        cout << "EVERYONE IS DEAD" << endl;
                }
                if (c != 0){
                        cout << "THERE ARE " << c << " PEOPLE LEFT" << endl;
                }
                a = 0;
        }
        else {
                a = 1;
        }
}
}

