#include <stdio.h>
#include <stdlib.h>
#define V 5 
#define E 7 

struct Edge {
    int src, dest, weight;
};

struct Subset {
    int parent, rank;
};

int find(struct Subset subsets[], int i) {
    if (subsets[i].parent != i)
        subsets[i].parent = find(subsets, subsets[i].parent);
    return subsets[i].parent;
}

void unionSets(struct Subset subsets[], int x, int y) {
    int xroot = find(subsets, x);
    int yroot = find(subsets, y);

    if (subsets[xroot].rank < subsets[yroot].rank)
        subsets[xroot].parent = yroot;
    else if (subsets[xroot].rank > subsets[yroot].rank)
        subsets[yroot].parent = xroot;
    else {
        subsets[yroot].parent = xroot;
        subsets[xroot].rank++;
    }
}

int compareEdges(const void* a, const void* b) {
    return ((struct Edge*)a)->weight - ((struct Edge*)b)->weight;
}

void kruskalMST(struct Edge edges[]) {
    struct Subset subsets[V];
    for (int i = 0; i < V; ++i) {
        subsets[i].parent = i;
        subsets[i].rank = 0;
    }

    qsort(edges, E, sizeof(edges[0]), compareEdges);

    struct Edge mst[V - 1];
    int mstSize = 0;

    for (int i = 0; i < E && mstSize < V - 1; ++i) {
        struct Edge edge = edges[i];
        int srcParent = find(subsets, edge.src);
        int destParent = find(subsets, edge.dest);

        if (srcParent != destParent) {
            mst[mstSize++] = edge;
            unionSets(subsets, srcParent, destParent);
        }
    }

    printf("Edge \t Weight\n");
    for (int i = 0; i < mstSize; ++i) {
        printf("%d - %d \t %d\n", mst[i].src, mst[i].dest, mst[i].weight);
    }
}

int main() {
    struct Edge edges[E] = {
        {0, 1, 2},
        {0, 3, 6},
        {1, 2, 3},
        {1, 3, 8},
        {1, 4, 5},
        {2, 4, 7},
        {3, 4, 9}
    };

    kruskalMST(edges);

    return 0;
}
