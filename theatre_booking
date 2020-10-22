#include<bits/stdc++.h>
#include<string>
using namespace std;

class Screen{
    int nRows;
    int nCols;
    set<int> aisle;
    
    int **grid;
    public:
    
    Screen(int nRows, int nCols, set<int> aisle){
        this->nRows = nRows;
        this->nCols = nCols;
        this->aisle = aisle;
            
        grid = new int*[nRows+1];
        for(int i=0;i<=nRows;i++){
            grid[i] = new int[nCols+1];
            for(int j=0;j<=nCols;j++)
                grid[i][j] = 0;
        }
    }
    
    int isReservePossible(int row, vector<int> &cols, int i){
        if(i==cols.size())
            return 1;
        
        if(cols[i]<=0 || cols[i]>this->nCols)
            return 0;
        
            
        if(this->grid[row][cols[i]])
            return 0;
        
        this->grid[row][cols[i]] = 1;
        if(isReservePossible(row, cols, i+1))
            return 1;
        
        this->grid[row][cols[i]] = 0;
        return 0;
        
    }
    void reserveSeats(int row, vector<int> &cols){
        if(row<=0 || row>this->nRows)
            return;
        
        if(isReservePossible(row, cols, 0))
            cout<<"success";
        else
            cout<<"failure";
    }
    
    void getUnreserved(int row){
        
        if(row<=0 || row>this->nRows)
            return;
            
        for(int i=1;i<=this->nCols;i++){
            if(!this->grid[row][i])
                cout<<i<<" ";
        }
    }
    
    void suggestSeats(int row, int nSeats, int preferredCol){
        if(row<=0 || row>this->nRows)
            return;
        
        if(preferredCol<=0 || preferredCol>this->nCols)
            return;
            
        //Check right
        int ans = 0;
        int seatsBooked = 0;
        int aisleBooked = 0;
        
        for(int i=preferredCol;i<=this->nCols;i++){
            int seat = this->grid[row][i];
            if(seat==0){
                seatsBooked++;
                if(seatsBooked==nSeats){
                    ans = aisleBooked==0;
                    break;
                }
            }
            else
                break;

            if(this->aisle.find(i)!=this->aisle.end())
                aisleBooked++;
        }
        
        if(!ans){
            for(int i=0;i<nSeats;i++){
                cout<<(i+preferredCol)<<" ";
            }
            return;
        }
        
        ans=0;
        seatsBooked=0;
        aisleBooked=0;
        //Check left
        for(int i=preferredCol;i>0;i--){
            int seat = this->grid[row][i];
            if(seat==0){
                seatsBooked++;
                if(seatsBooked==nSeats){
                    ans = aisleBooked==0;
                    break;
                }
                    
            }
            else
                break;
            if(this->aisle.find(i)!=this->aisle.end())
                aisleBooked++;
        }
        
        if(!ans){
            for(int i=0;i<nSeats;i++){
                cout<<(preferredCol-i)<<" ";
            }
            return;
        }
        cout<<"none";
    }
};

class theatre{
    public:
    unordered_map<string, Screen*> screens;
};


void doCommand(string s, theatre &t){
    vector<string> elements;
    string temp = "";
    for(int i=0;;i++){
        if(s[i]==' ' || s[i]=='\0'){
            elements.push_back(temp);
            temp="";
        }
        else{
            temp+=s[i];
        }
        if(s[i]=='\0')
            break;
    }
    
    string command = elements[0];
    
    if(command=="add-screen"){
        string name = elements[1];
        int nRows = stoi(elements[2]);
        int nCols = stoi(elements[3]);
        set<int> aisle;
        for(int i=4;i<elements.size();i++)
            aisle.insert(stoi(elements[i]));
            
        t.screens[name] = new Screen(nRows, nCols, aisle);
    }
    else if(command=="reserve-seat"){
        string name = elements[1];
        int row = stoi(elements[2]);
        vector<int> cols;
        for(int i=3;i<elements.size();i++)
            cols.push_back(stoi(elements[i]));
        
        t.screens[name]->reserveSeats(row, cols);
        cout<<"\n";
        
    }
    else if(command=="get-unreserved-seats"){
        string name = elements[1];
        int row = stoi(elements[2]);
        
        t.screens[name]->getUnreserved(row);
        cout<<"\n";
    }
    else if(command=="suggest-contiguous-seats")
    {
        string name = elements[1];
        int nSeats = stoi(elements[2]);
        int row = stoi(elements[3]);
        int preferredCol = stoi(elements[4]);
        
        t.screens[name]->suggestSeats(row, nSeats, preferredCol);
        cout<<"\n";
    }
}


int main(){
    int n;
    cin>>n;
    
    theatre t;
    for(int i=0;i<n;i++){
        string s;
        getline(cin, s);
        doCommand(s, t);
    }
    return 0;
}
