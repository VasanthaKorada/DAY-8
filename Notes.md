1.subset sum -using recursion,bit manipulation,and dp
----------------------------------------------
#include <bits/stdc++.h>
using namespace std;
int main() {
    int n; cin >> n;
    vector<int> v(n);
    for (int i = 0; i < n; i++) cin >> v[i];

    int k; cin >> k;

    vector<vector<int>> dp(n, vector<int>(k + 1, 0));

    for (int i = 0; i < n; i++) dp[i][0] = 1;

    if (v[0] <= k) dp[0][v[0]] = 1;

    for (int i = 1; i < n; i++) {
        for (int j = 1; j <= k; j++) {
            if (j < v[i]) {
                dp[i][j] = dp[i - 1][j];
            } else {
                dp[i][j] = dp[i - 1][j] || dp[i - 1][j - v[i]];
            }
        }
    }

    for (int i = 0; i < n; i++) {
        for (int j = 0; j <= k; j++) {
            cout << dp[i][j] << " ";
        }
        cout << "\n";
    }

    if (dp[n - 1][k])
        cout << "Subset with sum " << k << " is possible\n";
    else
        cout << "Subset with sum " << k << " is NOT possible\n";

    return 0;
}
2.SUBSET SUM WITH DUPLICATES
------------------------------------
#include <bits/stdc++.h>
using namespace std;
int main() {
    int n; cin >> n;
    vector<int> v(n);
    for (int i = 0; i < n; i++) cin >> v[i];

    int k; cin >> k;

    vector<vector<int>> dp(n, vector<int>(k + 1, 0));

    for (int i = 0; i < n; i++) dp[i][0] = 1;

    if (v[0] <= k) dp[0][v[0]] = 1;

    for (int i = 1; i < n; i++) {
        for (int j = 1; j <= k; j++) {
            if (j < v[i]) {
                dp[i][j] = dp[i - 1][j];
            } else {
                dp[i][j] = dp[i - 1][j] || dp[i - 1][j - v[i]];
            }
        }
    }

    for (int i = 0; i < n; i++) {
        for (int j = 0; j <= k; j++) {
            cout << dp[i][j] << " ";
        }
        cout << "\n";
    }

    if (dp[n - 1][k])
        cout << "Subset with sum " << k << " is possible\n";
    else
        cout << "Subset with sum " << k << " is NOT possible\n";

    return 0;
}
3.COIN CHANGE(when infinite are allowed)
----------------------------------------------
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n; cin >> n;
    vector<int> v(n);
    for (int i = 0; i < n; i++) cin >> v[i];

    int k; cin >> k;

    vector<vector<int>> dp(n, vector<int>(k + 1, 0));

    for (int i = 0; i < n; i++) dp[i][0] = 1;

    for (int j = 1; j <= k; j++) {
        if (j % v[0] == 0) dp[0][j] = 1;
    }

    for (int i = 1; i < n; i++) {
        for (int j = 1; j <= k; j++) {
            if (j < v[i]) {
                dp[i][j] = dp[i - 1][j];
            } else {
                dp[i][j] = dp[i - 1][j] || dp[i][j - v[i]];
            }
        }
    }

    for (int i = 0; i < n; i++) {
        for (int j = 0; j <= k; j++) {
            cout << dp[i][j] << " ";
        }
        cout << "\n";
    }

    if (dp[n - 1][k])
        cout << "Subset with sum " << k << " is possible\n";
    else
        cout << "Subset with sum " << k << " is NOT possible\n";

    return 0;
}


4.OPTIMIZED VERSION OF ABOVE
-------------------------------------------------------
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n; cin >> n;
    vector<int> v(n);
    for (int i = 0; i < n; i++) cin >> v[i];

    int k; cin >> k;

    vector<int> dp(k + 1, 0);
    dp[0] = 1;  
int f=0;
    for (int i = 0; i < n; i++) {
        int coin = v[i];
        f=0;
        for (int j = coin; j <= k; j++) {
            if (dp[j - coin] == 1) {
                dp[j] = 1;
                f=1;
            }

        }
        if(f==0)
        break;
      
    }

    if (dp[k] == 1)
        cout << k << " is possible\n";
    else
        cout << k << " is NOT possible\n";

    return 0;
}
5.MINIMUM NUMBER OF COINS NEEDED USING DP
------------------------------------------------------
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n; cin >> n;
    vector<int> v(n);
    for (int i = 0; i < n; i++) cin >> v[i];

    int k; cin >> k;

    vector<int> dp(k + 1, 0);
    dp[0] = 0;  
int f=0;
    for (int i = 0; i < n; i++) {
        int coin = v[i];
        f=0;
        for (int j = coin; j <= k; j++) {
            if(j==v[i])
            dp[j]=1;
            if (dp[j-v[i]]!=0 && dp[j]!=0) {
                dp[j]=min(dp[j-v[i]]+1,dp[j]);
              
            }
            
            if (dp[j-v[i]]!=0 && dp[j]==0)
            {
                dp[j]=dp[j-v[i]];
            }

        }
        
    }

    cout<<dp[k]<<endl;
      

    return 0;
}
6.Lnegth of the longest subsequence using DP
---------------------------------------------------
#include<bits/stdc++.h>
using namespace std;
int main(){
    string s,ss;
    cin>>s>>ss;
    int a=s.length();
    int b=ss.length();
    vector<vector<int>>dp(a+1,vector<int>(b+1,0));
    /* dp[0][0]=1;
     for(int i=0;i<=a;i++){
        dp[i][0]=1;    }
         for(int i=0;i<=b;i++){
       dp[0][i]=1;    }
       */
        for(int i=1;i<=a;i++){
            for(int j=1;j<=b;j++){
                if(s[i-1]==ss[j-1])
                {
                    dp[i][j]=dp[i-1][j-1]+1;
                }
                else{
                    dp[i][j]=max(dp[i][j-1],dp[i-1][j]);
                }
            }
        }
        cout<<dp[a][b];
}
