---
published: true
---
## Hackerrank - Insert a Node at a specific position in a Linked List

Arkayadır önedir derken en sonunda da istediğimiz yere ekleme yapmak istiyoruz.


### Noluyor?

İlk öncelikle bir bakalım ne oluyor.
![Linkedlist_insert_at_pos.png]({{site.baseurl}}/images/linked_list/Linkedlist_insert_at_pos.png)

Yani, istediğimiz yere ekleyeceksek bize bu pozisyonun solunda ve sağında bulunan **node**lar lazım ki, solda bulunan **nodu**n **next**ini bizim ekleyeceğimiz **node** yapalım, sağdakini de bizim ekleyeceğimiz **nodenin nexti**.

### Çözüm

{% highlight python %}
def insertNodeAtPosition(head, data, position):
    currentPos = 0 # şimdiki pozisyonumuz 0 bir zahmet yani
    currentNode = head # head imizin None olup olmadığına bakmaya lüzum yok
    # problemimiz zaten bize verilen bir bağlı listede ekleme yapmamızı istiyor
    # while döngümüzle bizden eklemek istediğimiz yerin bir öncesini buluyoruz
    while (currentNode.next != None and currentPos<position-1):
        currentPos += 1
        currentNode = currentNode.next
    # yeni nodemizi oluşturalım
    newNode = SinglyLinkedListNode(data)
    # eklemek istediğimiz yerin bir öncesinde bulunan nodenin sonrasını alalım
    nextNode = currentNode.next
    # eklemek istediğimiz yerin bir öncesinde bulunan nodenin sonrasını
    # yeni nodemiz yapalım
    currentNode.next = newNode
    # yeni nodemizin sonrasınıda eklemek istediğimiz yerin bir öncesinde bulunan 
    # nodenin sonrasında bulunan node yapalım (yazarken başım döndü açıkcası)
    newNode.next = nextNode
    # en sonunda headimizi returnlayalım
    return head
{% endhighlight %}

