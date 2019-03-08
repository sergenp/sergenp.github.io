---
published: true
layout: post
categories: Python
tags:
  - algoritma
  - bağlı liste
---
![reverse_linked_list.png]({{site.baseurl}}/images/linked_list/reverse_linked_list.png)

Yukarıdaki isteneni nasıl yapacağız? Bu sefer yazarak değil de bir videodan çaldığım ve gif yaptığım mp4 dosyası üzerinden anlatalım:
![reverse_list.gif]({{site.baseurl}}/images/linked_list/reverse_list.gif)

### Çözüm?

2 tane çözüm var, biri iteratif ve diğeri de recursive. Ben sadece iteratifini paylaşacağım. Siz de artık recursive versiyonunu yaparsınız(ben yapamadım).

#### İteratif Çözüm

{% highlight python %}
def reverse(head):
       oncekiNode = None
       simdikiNode = head
       sonrakiNode = simdikiNode.next
       while simdikiNode is not None:
           simdikiNode.next = oncekiNode       
           oncekiNode = simdikiNode
           simdikiNode = sonrakiNode
           if sonrakiNode is not None:
               sonrakiNode = sonrakiNode.next
       return oncekiNode
{% endhighlight %}
