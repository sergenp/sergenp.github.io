---
published: true
title: Hackerrank - Insert a Node at the Tail of a Linked List
layout: post
categories: Python
tags:
  - algoritma
  - bağlı liste
  - hackerrank
---
## Insert a Node at the Tail of a Linked List - Hackerrank

[Linked List(Bağlı Liste)](http://bilgisayarkavramlari.sadievrenseker.com/2007/05/03/linked-list-linkli-liste-veya-bagli-liste/) bir veri yapısı. Adındanda anlaşıldığı gibi birbirine bağlı listeler.

![linked_list.jpeg]({{site.baseurl}}/images/linked_list/linked_list.jpeg)

Bu listenin en sonuna eleman eklememizi istiyorlar. Kod olaraktan nasıl gözüküyor bu liste?

{% highlight python %}

class SinglyLinkedListNode:
    def __init__(self, node_data):
        self.data = node_data
        self.next = None

class SinglyLinkedList:
    def __init__(self):
        self.head = None
        
def print_singly_linked_list(node, sep, fptr):
    while node:
        fptr.write(str(node.data))
        node = node.next
        if node:
            fptr.write(sep)
{% endhighlight %}

Peki bu listenin sonuna nasıl ekleme yapacağız?
### Çözüm
{% highlight python %}
def insertNodeAtTail(head, data):
    if head == None:
        head = SinglyLinkedListNode(data)
    else:
        current = head
        while current.next != None:
            current = current.next
        current.next = SinglyLinkedListNode(data)
    return head
{% endhighlight %}


### Noluyor?
Açıklamak gerekirse, fonksiyonumuz listenin başını(head) ve ekleyeceğimiz data yı alıyor. Eğer bizim headimiz **None** ise, yani Listede hiçbişey yok ise, yeni bir **Node** yaratıp headimizi bu yapıyoruz.
{% highlight python %}
def insertNodeAtTail(head, data):
    if head == None:
        head = SinglyLinkedListNode(data)
{% endhighlight %}

Eğer headimiz **None** değilse, demekki headimiz var. Şuanki Node(current) imizi Head olarak alıyoruz, ve şuanki nodemizden sonra başka bir **Node** var mı diye bakıyoruz, bunun sebebi listenin en sonuna ekleme yapmamız, eğer başka **Node** varsa Son **Node** şimdiki **Node** umuz olmaz.

En son **Node** mizi bulunca bu **Node** nin sonrasında(next) **None** olduğunu biliyoruz. Ve bu Node mizin sonrasına yine bir **Node** oluşturup, verilen **data**mızı **yeni oluşturduğumuz Node** a atıyoruz.
{% highlight python %}
    else:
        current = head
        while current.next != None:
            current = current.next
        current.next = SinglyLinkedListNode(data)
    return head
{% endhighlight %}

En sonunda da **Head Node** umuzu return ediyoruz.
