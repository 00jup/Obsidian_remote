```python
# 콜백 방식
def fetch_data(callback):
    data = get_data()
    def process_data(callback):
        result = process(data)
        def save_data(callback):
            saved = save(result)
            callback(saved)
        save_data(callback)
    process_data(callback)

fetch_data(lambda x: print(x))

# 코루틴 방식  
async def handle_data():
    data = await get_data()
    result = await process(data)
    saved = await save(result)
    print(saved)

# 실제 예시
async def get_user_info():
    user = await db.fetch_user()
    posts = await db.fetch_posts(user.id) 
    likes = await db.fetch_likes(posts)
    return {
        'user': user,
        'posts': posts,
        'likes': likes
    }
```

코루틴 사용 시:
1. 비동기 작업을 위아래로 읽기 쉽게 작성
2. with/try-except 등 일반 구문 사용 가능  
3. 각 단계가 명확히 구분됨