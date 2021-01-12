# QuarySet 명령어 

In [1]: from blog.models import Post

In [2]: Post.objects.all()
Out[2]: <QuerySet [<Post: 첫번째 글>, <Post: 두번째 글>]>

In [3]: from django.contrib.auth.models import User

In [4]: User.objects.all()
Out[4]: <QuerySet [<User: admin>]>

In [5]: User.objects.get(username='admin')
Out[5]: <User: admin>

In [6]: me = User.objects.get(username='admin')

In [7]: me.username
Out[7]: 'admin'

In [8]: me.email
Out[8]: 'admin@aa.com'

In [9]: me.password
Out[9]: 'pbkdf2_sha256$216000$0ShJy5KAGHIn$HyK05n7YN3HrgT+ONRqdpi2ZD9QwIdmZkm2eva9mJls='

In [10]: me.id
Out[10]: 1

In [11]: Post.objects.create(author=me, title='Sample title', text='Test')
Out[11]: <Post: Sample title>

In [12]: Post.objects.all()
Out[12]: <QuerySet [<Post: 첫번째 글>, <Post: 두번째 글>, <Post: Sample title>]>

In [13]: Post.objects.filter(author=me)
Out[13]: <QuerySet [<Post: 첫번째 글>, <Post: 두번째 글>, <Post: Sample title>]>

In [14]: Post.objects.filter(title__contains='title')
Out[14]: <QuerySet [<Post: Sample title>]>

In [15]: mypost = Post.objects.filter(title__contains='title')

In [16]: mypost
Out[16]: <QuerySet [<Post: Sample title>]>

In [17]: type(mypost)
Out[17]: django.db.models.query.QuerySet

In [18]: for val in mypost:
    ...:     print(val)
    ...: 
Sample title

In [19]: myposts = Post.objects.filter(title__contains='글')

In [20]: myposts
Out[20]: <QuerySet [<Post: 첫번째 글>, <Post: 두번째 글>]>

In [21]: type(myposts)
Out[21]: django.db.models.query.QuerySet

In [22]: for post in mypost:
    ...:     print(type(post), post.id)
    ...: 
<class 'blog.models.Post'> 3

In [23]: from django.utils import timezone

In [24]: timezone.now()
Out[24]: datetime.datetime(2021, 1, 12, 8, 20, 11, 198439, tzinfo=<UTC>)

In [25]: Post.objects.filter(published_date__lte=timezone.now())
Out[25]: <QuerySet [<Post: 두번째 글>]>

In [26]: post3 = Post.objects.get(title="Sample title")

In [27]: post3.id
Out[27]: 3

In [28]: post3.text
Out[28]: 'Test'

In [29]: post3.published_date

In [30]: post3.publish()

In [31]: post3.published_date
Out[31]: datetime.datetime(2021, 1, 12, 8, 25, 24, 969787, tzinfo=<UTC>)

In [32]: Post.objects.filter(published_date__lte=timezone.now())
Out[32]: <QuerySet [<Post: 두번째 글>, <Post: Sample title>]>

In [33]: Post.objects.order_by('created_date')
Out[33]: <QuerySet [<Post: 첫번째 글>, <Post: 두번째 글>, <Post: Sample title>]>

In [34]: Post.objects.order_by('-created_date')
Out[34]: <QuerySet [<Post: Sample title>, <Post: 두번째 글>, <Post: 첫번째 글>]>

In [35]: Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
Out[35]: <QuerySet [<Post: 두번째 글>, <Post: Sample title>]>

In [36]: Post.objects.filter(published_date__lte=timezone.now()).order_by('-published_date')
Out[36]: <QuerySet [<Post: Sample title>, <Post: 두번째 글>]>

In [37]: from django.shortcuts import get_object_or_404

In [38]: get_object_or_404(Post,pk=1)
Out[38]: <Post: 첫번째 글>

In [39]: post1 = get_object_or_404(Post, pk=1)

In [40]: type(post1)
Out[40]: blog.models.Post

In [41]: post1.title
Out[41]: '첫번째 글'

In [42]: post1.created_dates
Out[42]: datetime.datetime(2021, 1, 12, 6, 22, 54, tzinfo=<UTC>)

In [43]: delpost = Post.objects.get(title='Sample title')

In [44]: delpost
Out[44]: <Post: Sample title>

In [45]: delpost.delete()
Out[45]: (1, {'blog.Post': 1})

In [46]: Post.objects.all()
Out[46]: <QuerySet [<Post: 첫번째 글>, <Post: 두번째 글>]>

