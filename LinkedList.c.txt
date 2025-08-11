#define _CRT_SECURE_NO_WARNINGS

#include <stdio.h>
#include <malloc.h>
#include <stdlib.h>

typedef struct ListNode
{
	int num;
	struct ListNode* next;
}LIST;

void Add_Rear_Num(LIST* LinkedList, int new_num);
void Print_All(LIST* LinkedList);
void Delete_Rear_Num(LIST* LinkedList);
int Count_List(LIST* LinkedList);

int main(void)
{
	int choose = 1;
	int new_num;

	LIST* head = malloc(sizeof(LIST));
	head->num = NULL;
	head->next = NULL;
	while (choose != 0)
	{
		printf("기능 선택 - 0번 종료, 1번 추가, 2번 출력, 3번 삭제, 4번 갯수세기: ");
		scanf("%d", &choose);
		switch (choose)
		{
		case 1:
			printf("추가할 숫자 입력 : ");
			scanf("%d", &new_num);
			Add_Rear_Num(head, new_num);
			break;
		case 2:
			Print_All(head);
			break;
		case 3:
			Delete_Rear_Num(head);
			break;
		case 4:
			printf("데이터 수 : %d\n", Count_List(head));
			break;
		default:
			printf("잘못된 입력입니다\n");
			break;
		}
	}
	return 0;
}

void Add_Rear_Num(LIST* LinkedList, int new_num) //마지막에 새 노드 추가
{
	LIST* temp;
	temp = LinkedList;

	if (temp->num == NULL) //최초 입력일 때
	{
		temp->num = new_num;
	}
	else
	{
		LIST* Newnode = malloc(sizeof(LIST));

		while (temp->next != NULL)
		{
			temp = temp->next;
		}
		temp->next = Newnode;
		Newnode->next = NULL;
		Newnode->num = new_num;
	}
}

void Print_All(LIST* LinkedList) //리스트 전체 출력
{
	if (Count_List(LinkedList) == 0)
	{
		printf("리스트가 비어있습니다\n");
	}
	else
	{
		LIST* temp;
		temp = LinkedList;
		while (temp)
		{
			printf("%d ", temp->num);
			temp = temp->next;
		}
		printf("\n");
	}

}

void Delete_Rear_Num(LIST* LinkedList)
{
	LIST* temp1 = LinkedList;
	LIST* temp2 = LinkedList;
	if (Count_List(LinkedList) == 0)
	{
		printf("리스트가 비어있습니다\n");
	}
	else if (Count_List(LinkedList) == 1)
	{
		LinkedList->num = NULL;
	}
	else
	{
		while (temp1->next->next != NULL)
		{
			temp1 = temp1->next;
		}
		while (temp2->next != NULL)
		{
			temp2 = temp2->next;
		}
		temp1->next = NULL;
		free(temp2);
	}

}

int Count_List(LIST* LinkedList)
{
	int count = 1;
	LIST* temp = LinkedList;
	if (temp->num == NULL)
	{
		return 0;
	}
	while (temp->next != NULL)
	{
		temp = temp->next;
		count++;
	}
	return count;
}