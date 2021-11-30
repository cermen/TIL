# 페이지네이터

페이지를 관리하는 클래스

```python
# pybo/views.py
def index(request):
    # 입력 파라미터
    page = request.GET.get('page', '1')

    # 조회
    question_list = Question.objects.order_by('-create_date')

    # 페이징 처리
    paginator = Paginator(question_list, 10)
    page_obj = paginator.get_page(page)

    context = {'question_list': page_obj}
    return render(request, 'pybo/question_list.html', context)
```

```html
<!-- templates/pybo/question_list.html -->
<!-- 페이징처리 시작 -->
    <ul class="pagination justify-content-center">
        <!-- 이전 페이지 -->
        {% if question_list.has_previous %}
        <li class="page-item">
            <a class="page-link" href="?page={{ question_list.previous_page_number }}">이전</a>
        </li>
        {% else %}
        <li class="page-item disabled">
            <a class="page-link" tabindex="1" aria-disabled="true" href="#">이전</a>
        </li>
        {% endif %}
        <!-- 페이지리스트 -->
        {% for page_number in question_list.paginator.page_range %}
        {% if page_number >= question_list.number|add:-5 and page_number <= question_list.number|add:5 %}
        {% if page_number == question_list.number %}
        <li class="page-item active" aria-current="page">
            <a class="page-link" href="?page={{ page_number }}">{{ page_number }}</a>
        </li>
        {% else %}
        <li class="page-item">
            <a class="page-link" href="?page={{ page_number }}">{{ page_number }}</a>
        </li>
        {% endif %}
        {% endif %}
        {% endfor %}
        <!-- 다음 페이지 -->
        {% if question_list.has_previous %}
        <li class="page-item">
            <a class="page-link" href="?page={{ question_list.next_page_number }}">다음</a>
        </li>
        {% else %}
        <li class="page-item disabled">
            <a class="page-link" tabindex="1" aria-disabled="true" href="#">다음</a>
        </li>
        {% endif %}
    </ul>
```