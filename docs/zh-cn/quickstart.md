# ��ʼ

## ����

django-echarts��һ����pyecharts���ϵ�Django������Ӧ�ð�(Django App)����Ҫ�У�

- ���ݹ�������
- ����ǰ�˻��˵�������Ⱦ
- js��̬�ļ�����
- ���õ������

## ��װ

django-echarts�İ�װҪ��Ϊ��

- Python2.7+����3.5+
- Django 1.8+
- pyecharts 0.3.0+

���Դ�pypi��װ

```
pip install django-echarts
```

����ʹ��Դ�빹��

```shell
git clone https://github.com/kinegratii/django-echarts.git
cd django-echarts
python setup.py install
```

## ����ʹ��

1 ��� django_echarts������Ŀ����ģ��� `INSTALL_APPS`�б�

```python
INSTALL_APPS = (
    # Your apps
    'django_echarts',
    # Your apps
)
```

2 ����ʵ�ʳ�����Ҫ����һЩ���ò�������Щ�������붨������Ŀģ����һ����Ϊ `DJANGO_ECHARTS` ���ֵ��

```python
DJANGO_ECHARTS = {
    'lib_js_host':'cdnjs'
}
```

����ȫ������Ĭ��ֵ�������ѡֵ��� API �ĵ���

3 ������Ⱦ��ʽ��ǰ�˻��ߺ�˷�ʽ����д��ͼ�࣬ģ��ҳ���·�ɡ�

ǰ����Ⱦ��ʽ

```python
def create_simple_bar():
    bar = Bar("�ҵĵ�һ��ͼ��", "�����Ǹ�����")
    bar.add("��װ", ["����", "��ë��", "ѩ����", "����", "�߸�Ь", "����"], [5, 20, 36, 10, 75, 90])
    return bar


class SimpleBarView(EChartsFrontView):
    def get_echarts_instance(self, **kwargs):
        return create_simple_bar()
      
```

�����Ⱦ��ʽ

```python
 class BackendEChartsTemplate(EChartsBackendView):
    template_name = 'backend_charts.html'

    def get_echarts_instance(self, *args, **kwargs):
        return create_simple_bar()
```

4 ��дģ���ļ�������ʹ����ر�ǩ��������`echarts`��ǩ�����ȾJS���ݡ�

```html
{% extends 'base.html' %}
{% load echarts %}

{% block main_content %}
    <div class="row row-offcanvas row-offcanvas-right">
        <div class="col-xs-6 col-sm-2 sidebar-offcanvas" id="sidebar">
            <div class="list-group">
                <a href="?name=bar" class="list-group-item">����ͼ(Bar)</a>
                <a href="?name=kine" class="list-group-item">K��ͼ(KLine)</a>
                <a href="?name=map" class="list-group-item">��ͼ(Map)</a>
                <a href="?name=pie" class="list-group-item">��ͼ(Pie)</a>
            </div>
        </div>
        <!--/.sidebar-offcanvas-->
        <div class="col-xs-12 col-sm-10">
            <p class="pull-right visible-xs">
                <button type="button" class="btn btn-primary btn-xs" data-toggle="offcanvas">Toggle nav</button>
            </p>
            {# ��Ⱦ���� #}
            {% echarts_container echarts_instance %}

        </div>
        <!--/.col-xs-12.col-sm-9-->
    </div>

{% endblock %}

{% block extra_script %}
    {# ��Ⱦ�����ļ� #}
    {% echarts_js_dependencies echarts_instance %} 
    {# ��Ⱦ��ʼ���ı� #}
    {% echarts_js_content echarts_instance %}
{% endblock %}
```

5 �ڲ�����ʽ����ʱ�������Ҫʹ�ù���CDN�йܳ���JS�ļ������޸���Ŀ���ã�ʹ�� `lib_js_host`����`map_js_host`ָ�򹫹�CDN��