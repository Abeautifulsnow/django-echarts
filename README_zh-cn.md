# django-echarts

![django-echarts version](https://img.shields.io/pypi/v/django-echarts.svg) ![python27](https://img.shields.io/badge/Python-2.7+-blue.svg) ![python35](https://img.shields.io/badge/Python-3.5+-blue.svg) ![django18](https://img.shields.io/badge/Django-1.8+-blue.svg)

���� [chenjiandongx/pyecharts](https://github.com/chenjiandongx/pyecharts) �� [Echarts](http://echarts.baidu.com/index.html)�� [Django](https://www.djangoproject.com) �����Ͽ⡣

> Ŀǰ����Ŀ�����ڿ���״̬��������������������ʹ�á�


## ����Ҫ��

- Python2.7+ / Python3.5+
- Django 1.8+
- echarts 3.1+

## ����ʹ��

views.py

```python
from django.views.generic.base import TemplateView
from pyecharts import Bar
from django_echarts import EchartsView

class IndexView(TemplateView):
    template_name = 'index.html'

class SimpleBarView(EchartsView):
    def get_echarts_option(self, **kwargs):
        bar = Bar("�ҵĵ�һ��ͼ��", "�����Ǹ�����")
        bar.add("��װ", ["����", "��ë��", "ѩ����", "����", "�߸�Ь", "����"], [5, 20, 36, 10, 75, 90])
        return bar._option
```

urls.py

```python
from django.conf.urls import url

from .views import IndexView, SimpleBarView

urlpatterns = [
    url(r'^$', IndexView.as_view()),
    url(r'options/simpleBar/', SimpleBarView.as_view())
]
```

html

```html
<div id="id_echarts_container" style="height: 500px;"></div>

<script type="text/javascript">
    $(document).ready(function () {
        var mChart = echarts.init(document.getElementById('id_echarts_container'));
        $.ajax({
            url: '/options/simpleBar/',
            type: "GET",
            dataType: "json"
        }).done(function (data) {
            mChart.setOption(data);
        });
    });
</script>
```

## API

(����)

## ʾ��

ʾ����Ŀ��ο� example �ļ��С�

```shell
cd example
python manage.py runserver 127.0.0.1:8000
```

���ʱ��ص�ַ�� http://127.0.0.1:8000 ��ʾ�����н��

![Demo](images/demo1.gif)

## ��ԴЭ��

��Ŀ���� MIT��ԴЭ�飬��ӭ�ύ Issue & Pull request ��