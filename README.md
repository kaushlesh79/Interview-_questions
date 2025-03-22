# Interview-_questions
in this repo i will add questions which i faced during interview rounds of any company




## Topic : Graph , Toposort Pattern (Asked By Zupee )  [ Role : SDE backend]

Question --->

Given list of objects-
{a, b, "right"} --> a is to the right of b
{c,b, "right"} --> c is to the right of b
{b,a, "left"} --> b is to the left of a

sort them based on left and right conditions.

output any valid output.
one valid output is - b, a, c


Solution ----->

```bash

#include<bits/stdc++.h>
using namespace std ; 


vector<string>toposort_pattern(vector<tuple<string , string , string>>&relation){
    
    unordered_map<string , vector<string>>adj; unordered_map<string , int>indegree ;
       unordered_set<string>nodes;// total nodes in graph it keep tracks of it 
       
       // build graph
       for (auto & [a , b , dir] : relation){
           
           nodes.insert(a);
           
           nodes.insert(b);
           
           if(dir == "left"){  // a comes before b 
           //means  b will depend upon a , to complete first 
               // a---->b
               
               
               adj[a].push_back(b);
               indegree[b]++;
               
               
           }else{
               
               adj[b].push_back(a);
               indegree[a]++;
           }
       }
       
       // now toposort
       
       queue<string>q;
       
       for(auto node : nodes){
           if(indegree[node]==0){
               q.push(node);
           }
       }
       vector<string>topo_order;
       while(!q.empty()){
           
           string curr=q.front();
           q.pop();
           
           topo_order.push_back(curr);
           
           for(auto nbr : adj[curr]){
               
               indegree[nbr]--;
               
               if(indegree[nbr]==0){
                   q.push(nbr);
               }
           }
       }
       return topo_order;
}

int main() {
    vector<tuple<string, string, string>> relations = {
        {"a", "b", "right"},  // b → a
        {"c", "b", "right"},  // b → c
        {"b", "a", "left"} ,   // b → a (same as first)
        {"d" , "c" , "right"},  // c---->d 
        
        {"e" , "b" , "left"}    // e---->b 
        // now b appears before averyone
    };

    vector<string> sortedOrder = toposort_pattern(relations);
    
    for (const string &s : sortedOrder) {
        cout << s << " ";
    }
    cout << endl;

    return 0;
}


```

