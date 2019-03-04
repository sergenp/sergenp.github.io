---
published: true
layout: post
categories: Python
tags:
  - algoritma
title: Hackerrank - Insert a node at the head of a linked list
---
##  Hackerrank - Insert a node at the head of a linked list

Linked listi önceki gönderimde göstermiştim.
![linked_list.jpeg]({{site.baseurl}}/images/linked_list/linked_list.jpeg)

Bize ekleyeceğimiz elemanın listenin başına eklememiz gerektiğini söylüyorlar.

Listenin başına nasıl ekleme yapacağız?
### Çözüm
{% highlight python %}
def insertNodeAtHead(llist_head, data):
    if llist_head is None:
        llist_head = SinglyLinkedListNode(data)
    else:
        currentHead = llist_head
        newNode = SinglyLinkedListNode(data)
        llist_head = newNode
        newNode.next = currentHead
    return llist_head
{% endhighlight %}


### Noluyor?
{% highlight python %}
def insertNodeAtHead(llist_head, data):
    if llist_head is None:
        llist_head = SinglyLinkedListNode(data)
{% endhighlight %}

Buradan anlaşılacağı üzeri eğer listenin **head** kısmı **None** ise(head de **data** yoksa) ekleyeceğimiz elemanı direk listenin başına atıyoruz
{% highlight python %}
    else:
        lastHead = llist_head
        newNode = SinglyLinkedListNode(data)
        llist_head = newNode
        newNode.next = lastHead
    return llist_head
{% endhighlight %}

Bu kısımda ise basit bir "**swap**" işlevi yaptığımızı düşünün, listenin son **head**ini bir değişkende(lastHead) tutuyoruz, yeni nodemizi(**newNode**) verilen data ya göre oluşturuyoruz, listenin **head**ine oluşturduğumuz **newNode** yi atıyoruz ve bu **NewNode**nin sonraki elemanını listenin eski headine atıyoruz