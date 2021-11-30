# 답변 갯수 표시

```html
<!-- templates\pybo\question_list.html -->
<td>
    <a href="{% url 'pybo:detail' question.id %}">{{ question.subject }}</a>
    {% if question.answer_set.count %}
    <span class="text-danger small ml-2">{{ question.answer_set.count }}</span>
    {% endif %}
</td>
```