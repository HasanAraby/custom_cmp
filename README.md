# custom_cmp


#pragma GCC optimze "trapv"
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define en '\n'
#define F first
#define S second
#define tasree ios_base::sync_with_stdio(0), cin.tie(0), cout.tie(0)
#define all(x) x.begin(), x.end()
#define rall(x) x.rbegin(), x.rend()
#define sz(x) int(x.size())

const int N = 2e5 + 5, M = 55, mod = 998244353, MX = 2e9;
// initialization: int a, int b    logic: return a < b   result: ascending
// initialization: int a, int b    logic: return a > b   result: descending
// initialization: int b, int a    logic: return a < b   result: descending
// initialization: int b, int a    logic: return a > b   result: ascending
// descending
bool cmp(int a, int b)
{

    return a > b;
}

// ascending order
struct cmpClass
{
    bool operator()(int a, int b)
    {
        return a < b;
    }
};

// ascending order
template <class T>
struct genericCmpClass
{
    bool operator()(T a, T b)
    {

        if (a.F == b.F)
            return a.S > b.S;
        return a.F < b.F;
    }
};

bool customCompare(int a, int b)
{
    // Sorting odd numbers before even numbers
    if (a % 2 != b % 2)
    {
        return a % 2 > b % 2;
    }
    // If both numbers are odd or even, sort in ascending order
    return a < b;
}

void test()
{

    // sort will still o(nlogn) while using custom cmp
    vector<int> v;
    v.push_back(4);
    v.push_back(8);
    v.push_back(7);
    v.push_back(2);
    v.push_back(0);
    v.push_back(1);

    sort(all(v), cmp);
    cout << "descending cmp function" << en;
    for (auto i : v)
        cout << i << ' ';
    cout << en << en;

    sort(all(v), cmpClass());
    cout << "ascending cmp struct" << en;
    for (auto i : v)
        cout << i << ' ';
    cout << en << en;

    vector<pair<int, int>> pairs;
    pairs.push_back({3, 6});
    pairs.push_back({8, 3});
    pairs.push_back({8, 1});
    pairs.push_back({6, 0});
    pairs.push_back({8, 10});

    sort(all(v), customCompare);
    cout << "ascending odd before even" << en;
    for (auto i : v)
        cout << i << ' ';
    cout << en << en;

    sort(all(pairs), genericCmpClass<pair<int, int>>());
    cout << "ascending cmp template(generic) struct but descending second" << en;
    for (auto i : pairs)
        cout << i.F << ' ' << i.S << en;
    cout << en;

    priority_queue<int, vector<int>, cmpClass> pq;
    pq.push(3);
    pq.push(0);
    pq.push(6);

    // priority_queue , set, .. don't has sort function so it takes its sorting while declaration and takes class not object like vector
    cout << "priority_queue has different logic so you need to revese a, b or replace < with > to get ascending order" << en;
    while (pq.size())
    {

        int x = pq.top();
        cout << x << ' ';
        pq.pop();
    }
}
int main()
{
    tasree;

    int t = 1;
    // cin >> t;
    while (t--)
    {
        test();
    }
    return 0;
}


#output



descending cmp function
8 7 4 2 1 0 

ascending cmp struct
0 1 2 4 7 8 

ascending odd before even
1 7 0 2 4 8 

ascending cmp template(generic) struct but descending second
3 6
6 0
8 10
8 3
8 1

priority_queue has different logic so you need to revese a, b or replace < with > to get ascending order
6 3 0 
