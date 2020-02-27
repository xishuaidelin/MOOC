**链表**

typedef  struct polynode *polynomial;  //多项式结构

struct polynode {

​	int coef ;

​	int expon;

​	polynomial link;

}

线性表数组存储

typedef  struct Lnode *List;

struct Lnode {

​	ElementType Data[Maxsize];

​	int Last;      // length of  the table is L.Last+1 

}

struct Lnode L;

List ptrl;            //访问元素 L.Data[i] or ptrl->Data[i]

初始化

List MakeEmpty(){

​	List ptrl;

​	ptrl = (List ) malloc (sizeof(struct Lnode));

​	ptrl->Last=-1;

​	return ptrl;

}

查找

int Find(ElementType X, List ptrl){

​	int i=0;

​	while(i<=ptrl->Last &&ptrl -> Data[i]!=X) i++;

​	if (i>ptrl-> Last) return -1;

​	else return i;                       // 找到后返回下标

}

插入

void Insert (ElementType X, int i, List ptrl){

​	int j;

​	if(ptrl->Last==MAXSIZE-1){

​		printf("表满");

​		return;

​	}

​	if(i<1||i>ptrl->Last+2){

​		printf("位置不合法");

​		return;

​	} 

​	for(j=ptrl->Last;j>=i-1;j--)	ptrl->Data[j+1]=ptrl->Data[j];   //移动数组

​	ptrl->Data[i-1]=X;  	//新元素插入

​	ptrl-> Last++;        //指向最后一个元素

​	return ;

}

删除操作

void Delete(int i, List ptrl){	

​	int j;

​	if( i<1 ||i>ptrl->Last+1){

​		printf("不存在第%d个元素",i);

​		return;

​	}

​	for(j=i;j<=ptrl->Last;j++)  ptrl->Data[j-1]=ptrl-> Data[j];

​	ptrl->Last--;

​	return;

}

线性表链式存储

typedef struct Lnode *List;

struct Lnode{

​	ElementType Data;

​	List Next;

};

struct Lnode L;

List ptrl;

求表长度

int Length(List ptrl){

​	List p= ptrl;

​	int j=0;

​	while(p){

​		p=p->Next;

​		j++;

​	}

​	return j;

}

查找

序号查找

List FindKth(int K, List ptrl){

​	List p=ptrl;

​	int i=1;

​	while(p!=Null && i<K){

​		p=p->Next;

​		i++;

​	}

​	if(i==K) return p;

​	else return NULL;

}

按值查找

List Find(ElementType X, List ptrl){

​	List p=ptrl;

​	while(p!=NULL&&p->Data!=X) p=p->Next;  // last list元素的next值为null

​	return p;

}

插入操作

List Insert(ElementType X ,int i, List ptrl){

​	List p,s;

​	if(i==1){

​		s=(List )malloc(sizeof(struct Lnode));

​		s->Data = X;

​		s->Next = ptrl;

​		return s;

​	}

​	p=FindKth(i-1,ptrl);

​	if(p==NULL){

​		printf("参数i错")；

​		return NULL;

​	}else{

​		s=(List)malloc(sizeof(struct Lnode));

​		s->Data = X;

​		s->Next=p->Next;

​		p->Next= s;

​		return ptrl;

​	}

}

List Delete(int i,List ptrl){

​	List p,s;

​	if(i==1){

​		s=ptrl;

​		if(ptrl!=NULL) ptrl=ptrl->Next;

​		else return NULL;

​		free(s);

​		return ptrl;

​	}

​	p=FindKth(i-1,ptrl);

​	if(p==NULL){

​		printf("第%d个节点不存在"，i-1);    return NULL;

​	}else if(p->Next==NULL){

​		printf("第%d个节点不存在"，i);   return NULL;

​	}else{

​		s=p->Next;

​		p->Next=s->Next;

​		free(s);

​		return ptrl;

​	}

}

广义表（一个后面节点后面可以跟两个表：sublist & Next）

插播共用体(union)的内容： 将不同类型的数据组织在一起共同占用同一段内存的一种构造数据类型。共用体类型所占内存空间的大小取决于其成员中占内存空间最多的那个成员变量。union在每一瞬时起作用的成员就是最后一个被赋值的成员。

typedef struct Gnode *Glist;

struct Gnode{

​	int tag;    //标志域：0->结点为单元素

​	union{

​		ElementType Data;

​		Glist Sublist;

​	}URegion;

​	Glist Next;

}

**栈**

