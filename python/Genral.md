نکته‌های مربوط به پایتون 
---


نحوه تعریف یک متغیر
---
نوع‌ها توسط خود سیستم مشخص می‌شود.

```python
username = "ali"

articles = []

age=23

```


نحوه تعریف یک فانکشن
---
برای تعریف فانکشن نیازی به {}  نداریم. 
همچنین ;  هم نداریم

برای مشخص کردن اسکوپ از فرورفتگی استفاده می‌کنیم.


```python
def hello(name):
    print(name)
    
def bye():
    print 'bye'
    

```


تعریف کلاس
---

برای استفاده از هر ماژول باید آن را import  کنیم.

برای ساخت متد‌هایی که به instance  وابسته نیستند
و عضو کلاس‌  هستند از انوتیشن @classmethod  استفاده می‌کنیم.
متدهایی که یه این صورت هستند می‌توانند به صورت مستقیم و بدون ساخت نمونه از کلاس استفاده شوند.

```python

class Source(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.Text, nullable=True)
    subtitle = db.Column(db.Text, nullable=True)
    link = db.Column(db.Text, nullable=True)
    feed = db.Column(db.Text, nullable=True)
    date_added = db.Column(db.DateTime, default=datetime.datetime.utcnow())

    @classmethod
    def insert_from_feed(cls, feed, feed_source):
        link = feed_source['link']
        title = feed_source['title']
        subtitle = feed_source['subtitle']
        source = Source(feed=feed, link=link, title=title, subtitle=subtitle)
        db.session.add(source)
        db.session.commit()
        return source

```