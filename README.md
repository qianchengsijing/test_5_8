# test_5_8
#include <stdio.h>
//线索二叉树的存储结构
//辅助全局变量，用于查找p的前驱
typedef struct BiTNode{
	ElemType data;
	struct BiTNode *lchild,*rchild;
}BiTNode,*BiTree;
BiTNode *p;
BiTNode *Pre = NULL;
BiTNode *Final = NULL;
ThreadNode *Pre = NULL;
typedef struct ThreadNode{
	Elemtype data;
	struct ThreadNode *lchild,*rchild;
	int ltag,rtag;//tag为0表示指针指向孩子，为1指针为线索；
}TheadNode,*ThreadTree;
//中序遍历二叉树
void InThread(ThreadTree T){
	if(T != NULL)
	{
		InThread(T->lchild);
		visit(T);
		InThread(T->rchild);
	}
}
//先序遍历二叉树
void PreThread(ThreadTree T){
	if(T != NULL)
	{
		visit(T);
		if(T->ltag == 0)
		    PreThread(T->lchild);
		PreThread(T->rchild);
	}
}
//后序遍历二叉树
void PostThread(ThreadTree T){
	if(T != NULL)
	{
		PostThread(T->lchild);
		PostThread(T->rchild);
		visit(T);
	}
}
void visit(ThreadNode *q){
	if(q->lchild == NULL)
	{
		q->lchild = Pre;
		q->ltag = 1;
	}
	if(Pre != NULL && Pre->rchild == NULL)
	{
		Pre->rchild = p;
		Pre->rtag = 1;
	}
	Pre = q;
}
//中序线索化二叉树
void CreateInThread(ThreadTree T){
	Pre = NULL;
	if(T != NULL)//非空二叉树才可线索化
	{
		InThread(T);
		if(Pre->rchild == NULL)
			Pre->rtag = 1;//处理最后一个结点
	}
}
//王道教材版（中序线索化二叉树）
void InThread(ThreadTree p,ThreadTree &Pre){
	if(p != NULL)
	{
		InThread(p->lchild,Pre);
		if(p->lchild == NULL)
	    {
		    p->lchild = Pre;
		    p->ltag = 1;
	    }
	    if(Pre != NULL && Pre->rchild == NULL)
	    {
	     	Pre->rchild = p;
		    Pre->rtag = 1;
	    }
	    Pre = p;
		InThread(p->rchild,Pre);
	}
}
