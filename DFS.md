# DFS学习
## 一、走迷宫
```c++
#include <iostream>
#include <string>


int n, m;
std::string map[11];
bool vis[100][100];

bool dfs(int x, int y);

bool check_pos(int tx, int ty);

int main() {
    std::cin >> n >> m;
    for (int i = 0; i < n; i++) {
        std::cin >> map[i];
    }
    dfs(0, 0);

    for (int i = 0; i < n; ++i) {
        std::cout << map[i] << "\n";
    }
    return 0;
}

bool dfs(int x, int y) {
    if (map[x][y] == 'T') {
        return true;
    }
    char o = map[x][y];
    vis[x][y] = true;
    map[x][y] = 'm';

    int direction[][2] = {
            {-1, 0},
            {0,  -1},
            {0,  1},
            {1,  0}
    };

    for (int i = 0; i < 4; i++) {
        int tx = x + direction[i][0];
        int ty = y + direction[i][1];
        if (check_pos(tx, ty) && map[tx][ty] != '*' && !vis[tx][ty] && dfs(tx, ty)) {
            return true;
        }
    }
    vis[x][y] = false;
    map[x][y] = o;
    return false;
}

bool check_pos(int tx, int ty) {
    return tx >= 0 && tx < n && ty >= 0 && ty < m;
}

/*
    input:
     
    6 6
    .*****
    ...*.*
    ...***
    **.***
    .*.**.
    .*...T
     
     
    output:
     
    m*****
    mmm*.*
    ..m***
    **m***
    .*m**.
    .*mmmT

 */

```