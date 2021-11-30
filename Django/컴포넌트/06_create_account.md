# 계정 생성

1. 계정 생성을 위한 링크를 `common\login.html`에 작성한다.

   ```html
   <!-- common\login.html -->
   <div class="row">
       <div class="col-4">
           <h4>로그인</h4>
       </div>
       <div class="col-8 text-right">
           <span>또는 <a href="{% url 'common:signup' %}">계정을 만드세요.</a></span>
       </div>
   </div>
   ```

2. `commons/urls.py` 파일에 URL 매핑을 추가한다.

3. `commons/forms.py` 파일에 UserForm을 작성한다.

   ```python
   from django import forms
   from django.contrib.auth.forms import UserCreationForm
   from django.contrib.auth.models import User
   
   
   class UserForm(UserCreationForm):
       email = forms.EmailField(label="이메일")
   
       class Meta:
           model = User
           fields = ("username", "password1", "password2", "email")
   ```

   - `UserCreationForm`은 기본적으로 "username", "password1", "password2" 속성을 가진다
     => 이메일 등 부가 속성을 추가하기 위해 새 클래스를 상속하여 만든다.

4. `common/views.py`파일에 `signup` 함수를 정의한다.

   ```python
   from django.contrib.auth import authenticate, login
   from django.shortcuts import render, redirect
   from common.forms import UserForm
   
   
   # 계정 생성
   def signup(request):
       if request.method == 'POST':
           form = UserForm(request.POST)
           if form.is_valid():
               form.save()
               username = form.cleaned_data.get('username')
               raw_password = form.cleaned_data.get('password1')
               user = authenticate(username=username, password=raw_password)
               login(request, user)    # 로그인
               return redirect('index')
       else:
           form = UserForm()
       return render(request, 'common/signup.html', {'form': form})
   ```

5. `common/signup.html` 템플릿을 작성한다.

