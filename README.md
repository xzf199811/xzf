# xzf
平衡二叉树
struct Node//定义他们的节点
{
    int key;
    Node *left;//指向左子树
    Node *right;//指向右子树
};

int max(int a,int b);//构造比较大小的函数，方便计算树的高度，返回较大的那个
int get_height(Node *root);//得到以root为根节点的树的高度
int balancefactor(Node *root);//得到某一点的平衡因素数值
void left_rotation(Node *root);//左旋操作,以根节点为标准
void right_rotation(Node *root);//右旋操作，以根节点为标准
void insert(Node *&root,int val);//插入某个节点，同时内含判断ll,lr,rl,rr型的各种类型，同时对其进行调整
void MidShow(Node *root);//中序遍历输出
Node * createTree(int a[],int n);//创建平衡二叉树
void test();
void PreShow(Node *root);//先序遍历
Node * balance(Node *root);



#include "Midholder_Function.hpp"
//为了平衡二叉排序树而做的功能函数！
int max(int a,int b)//构造比较大小的函数，方便计算树的高度，返回较大的那个
{
    return((a>b)?a:b);
}
//思想：没有节点的话，高度为-1，根节点高度为0，树的高度为左子树或者右子树最高的那个
int get_height(Node *root)//得到以root为根节点的树的高度，没有节点高度为-1，根节点高度为0
{
    if(root == nullptr)
        return -1;
    return max(get_height(root->left),get_height(root->right))+1;//返回较高子树的高度
}
//平衡因数=左子树高度-右子树的高度
int balancefactor(Node *root)//得到某一点的平衡因素数值
{
    if(root)
    return get_height(root->left)-get_height(root->right);
    return 0;
}
//左旋操作，将根节点的右孩子的左孩子作为原来根的右孩子，将根节点变为它右孩子的左孩子，左旋是以根节点为基准的
void left_rotation(Node *root)//左旋操作,以根节点为标准
{
    Node * t=root->right;
    root->right=t->left;
    t->left=root;
    
}
//右旋操作，将根节点的左孩子的右孩子作为原来根的左孩子， 将根节点变为它左孩子的右孩子，右旋是以根节点为基准的
void right_rotation(Node *root)//右旋操作，以根节点为标准
{
    Node * t=root->left;
    root->left=t->right;
    t->right=root;

}
//比根节点小的放左子树，比根节点大的放右子树，同时插入时对其进行判断，并自行调整让它满足AVL树
void insert(Node * &root,int v)//插入某个节点，同时内含判断ll,lr,rl,rr型的各种类型，同时对其进行调整
{
    //没有节点则创建一个新节点，V比该节点的关键字小，则插入左子树，比关键字大插入右子树，
    if(root == NULL)//没有节点就初始化一个根节点
    {
        root= new Node[v];
        root->key=v;root->left=root->right=NULL;
    }
    
    
    else if(v < root->key)
    {
        insert(root->left,v);
        balance(root->left);
    }
    else if(v > root->key)
    {
       insert(root->right,v);
        balance(root->right);
    }
    else
        return;
}
Node * createTree(int a[],int n)
{
    Node *root=NULL;//初始化根节点
    int i=0;
    while(i<n)
    {
        insert(root,a[i]);
        i++;
    }
    return root;
}
void MidShow(Node *root)//中序遍历输出:左根右
{
   
    if(root == NULL)
        return ;
    MidShow(root->left);
    cout<<root->key<<" ";
    MidShow(root->right);
    
}
void PreShow(Node *root)
{
    if(root == NULL)
        return ;
    cout<<root->key<<" ";
    MidShow(root->left);
    MidShow(root->right);
    
}
void test()
{
    cout<<1<<endl;
}
Node *balance(Node *root)
{
    if(balancefactor(root)>1)//左子树那边不平衡
    {
        if(balancefactor(root->left)<0)//这种情况需要先对其左孩子左旋
            right_rotation(root->left);
        right_rotation(root);
    }
    else if(balancefactor(root)<-1)//右子树那边不平衡
    {
        if(balancefactor(root->right)>0)//该情况只需要左旋一次就行了
            right_rotation(root->right);
        left_rotation(root);
    }
    return root;
}
#include"Midholder_Function.hpp"
int main(int argc, const char * argv[])
{

    Node *root;
    int *p,n=0;
    p=new int[1];
    cout<<"您想要多少个数？"<<endl;
    cin>>n;
    srand((unsigned)time(NULL));
    for(int i=0;i<n;i++)
    {
        p[i]=rand()%1000000;
    }
     for(int i=0;i<n;i++)
         cout<<"第"<<i+1<<"个"<<p[i]<<endl;
    root=createTree(p, n);
    cout<<"中序遍历如下"<<endl;
    MidShow(root);
    cout<<"先序遍历如下"<<endl;
    PreShow(root);
    delete []p;
    return 0;
    
}
#include"Midholder_Function.hpp"
int main(int argc, const char * argv[])
{

    Node *root;
    int *p,n=0;
    p=new int[1];
    cout<<"您想要多少个数？"<<endl;
    cin>>n;
    srand((unsigned)time(NULL));
    for(int i=0;i<n;i++)
    {
        p[i]=rand()%1000000;
    }
     for(int i=0;i<n;i++)
         cout<<"第"<<i+1<<"个"<<p[i]<<endl;
    root=createTree(p, n);
    cout<<"中序遍历如下"<<endl;
    MidShow(root);
    cout<<"先序遍历如下"<<endl;
    PreShow(root);
    delete []p;
    return 0;
    
}
#include"Midholder_Function.hpp"
int main(int argc, const char * argv[])
{

    Node *root;
    int *p,n=0;
    p=new int[1];
    cout<<"您想要多少个数？"<<endl;
    cin>>n;
    srand((unsigned)time(NULL));
    for(int i=0;i<n;i++)
    {
        p[i]=rand()%1000000;
    }
     for(int i=0;i<n;i++)
         cout<<"第"<<i+1<<"个"<<p[i]<<endl;
    root=createTree(p, n);
    cout<<"中序遍历如下"<<endl;
    MidShow(root);
    cout<<"先序遍历如下"<<endl;
    PreShow(root);
    delete []p;
    return 0;
    
}
