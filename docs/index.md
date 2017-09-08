# Django-Echarts Document


## Basic Usage

### Use ajax render

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