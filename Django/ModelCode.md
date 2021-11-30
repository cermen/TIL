Create your views here.
select * from table ;
-> modelName.objects.all()

select * from table where id = xxxx;
-> modelName.objects.get(id = xxxx)
-> modelName.objects.filter(id = xxxx)

select * from table where id = xxxx and pwd = xxxx;
-> modelName.objects.get(id = xxxx , pwd = xxxx)
-> modelName.objects.filter(id = xxxx , pwd = xxxx)

select * from table where id = xxxx or pwd = xxxx;
-> modelName.objects.filter(Q(id = xxxx) | Q(pwd = xxxx))

select * from table where subject like '%공지%'
-> modelName.objects.filter(subject_icontains='공지')
select * from table where subject like '공지%'
-> modelName.objects.filter(subject_startswith='공지')
select * from table where subject like '%공지'
-> modelName.objects.filter(subject_endswith='공지')

insert into table values()
model(attr=value , attr=value)
model.save()

delete * from tableName where id = xxxx
-> modelName.objects.get(id=xxx).delete()

update tableName set attr = value where id = xxxxx
obj = modelName.objects.get(id=xxxxx)
obj.attr = value
obj.save() -- commit