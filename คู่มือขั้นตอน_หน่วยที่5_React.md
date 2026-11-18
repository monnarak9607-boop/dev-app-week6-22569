# คู่มือขั้นตอนการทำงาน หน่วยที่ 5: เริ่มต้นพัฒนา Frontend ด้วย React.js

รหัสวิชา 21901-2013 การออกแบบและพัฒนาเว็บไซต์ · ปวช.1 สาขาวิชาเทคโนโลยีสารสนเทศ

คู่มือนี้สรุปวิธีทำงาน 4 ชิ้นของหน่วยที่ 5 ตามลำดับที่ควรทำ

| ลำดับ | เอกสาร | รูปแบบ | คะแนนเต็ม | เวลา |
|---|---|---|---|---|
| 1 | ใบความรู้ที่ 5 | เรียนรู้และทำแบบฝึกหัดคนเดียว | 10 + 10 | ตามที่ครูกำหนด |
| 2 | ใบงานที่ 4 | ปฏิบัติคนเดียว | 5 | 2 ชั่วโมง |
| 3 | ใบกิจกรรมที่ 5 | ทำงานกลุ่ม 3-4 คน | 10 | ประมาณ 60 นาที |
| 4 | ใบมอบหมายงานที่ 5 | ทำคนเดียวนอกเวลา | 5 | ส่งคาบถัดไป |

---

## 0. เตรียมความพร้อมก่อนเริ่ม

1. ติดตั้ง Node.js และ Visual Studio Code
2. เปิด Terminal แล้วตรวจสอบเวอร์ชัน
   ```bash
   node -v
   npm -v
   ```
   ถ้าขึ้นหมายเลขเวอร์ชันทั้งสองคำสั่ง แสดงว่าพร้อมใช้งาน
3. ใช้ Chrome หรือ Edge เป็นเบราว์เซอร์ทดสอบ
4. เปิดใบความรู้ที่ 5 ไว้เปิดอ้างอิงระหว่างทำงาน

---

## 1. ใบความรู้ที่ 5: เรียนรู้และทำแบบฝึกหัด

### วิธีเรียน

1. อ่านหัวข้อ 5.1 เรื่อง SPA แล้วจำความต่างของ MPA กับ SPA
   - MPA: เซิร์ฟเวอร์ส่ง HTML หน้าใหม่ทุกครั้ง โหลดครั้งแรกเร็ว ทำ SEO ง่าย
   - SPA: โหลด `index.html` หน้าเดียว แล้วให้ JavaScript อัปเดตเฉพาะส่วนที่เปลี่ยน ลื่นไหลกว่า
2. อ่านหัวข้อ 5.2 เรื่องการสร้างโปรเจกต์ด้วย Vite แล้วจำคำสั่ง 4 บรรทัดและหน้าที่ของไฟล์
3. อ่านหัวข้อ 5.3 เรื่อง JSX, Component และ Props แล้วจำ 4 กฎของ JSX
   - มี Root Element ตัวเดียว
   - ปิดแท็กให้ครบ
   - ใช้ `className` แทน `class`
   - แทรกค่า JavaScript ด้วย `{ }`
4. ดูตารางข้อผิดพลาดที่พบบ่อย (5.3.5) เพราะมักออกเป็นข้อสอบ

### วิธีทำแบบฝึกหัด

**ตอนที่ 1 (10 ข้อ ข้อละ 1 คะแนน)**
อ่านโจทย์ ตัดตัวเลือกที่ผิดอย่างชัดเจนออกก่อน แล้วเลือกข้อที่ถูกที่สุดเพียงข้อเดียว

**ตอนที่ 2 (2 ข้อ ข้อละ 5 คะแนน)**

*ข้อ 1 เขียน Component Greeting*

```jsx
function Greeting({ name }) {
  return <p>สวัสดี {name}</p>
}

function App() {
  return (
    <div>
      <Greeting name="สมชาย" />
      <Greeting name="สมหญิง" />
    </div>
  )
}

export default App
```

*ข้อ 2 หาข้อผิดพลาด 3 จุด* ให้ไล่ตรวจตามลำดับนี้

1. ชื่อ Component ขึ้นต้นด้วยตัวพิมพ์เล็ก (`postcard`) ต้องแก้เป็น `PostCard`
2. ใช้ `class` ต้องแก้เป็น `className`
3. return มี Root Element 2 ตัว (`<h2>` กับ `<p>`) ต้องห่อด้วย `<div>` หรือ Fragment `<> </>`

---

## 2. ใบงานที่ 4: สร้างและใช้งาน Component + Props

**เป้าหมาย:** สร้างโปรเจกต์ `blog-app` ที่แสดงรายการบทความด้วย Component และ Props

**ต้องส่ง:** ภาพหน้าจอ 2 ภาพ และไฟล์ .zip ของโฟลเดอร์ `blog-app` (ไม่รวม `node_modules`)

### ขั้นที่ 1 สร้างโปรเจกต์ด้วย Vite

```bash
npm create vite@latest blog-app -- --template react
cd blog-app
npm install
```

ถ้ามีคำถามให้เลือก **React** และ **JavaScript**

### ขั้นที่ 2 รัน Development Server

```bash
npm run dev
```

เปิดเบราว์เซอร์ที่ `http://localhost:5173` แล้ว **ถ่ายภาพหน้าจอเป็นหลักฐานที่ 1**

### ขั้นที่ 3 ล้างโค้ดเริ่มต้น

1. เปิดโฟลเดอร์ `blog-app` ด้วย VS Code
2. แก้ `src/App.jsx` ให้เหลือเท่านี้
   ```jsx
   function App() {
     return (
       <main>
         <h1>My Blog</h1>
       </main>
     )
   }

   export default App
   ```
3. ลบเนื้อหาในไฟล์ `src/App.css`
4. ลบบรรทัด `import './App.css'` ถ้ามี

### ขั้นที่ 4 สร้าง Component Header

สร้างโฟลเดอร์ `src/components` แล้วสร้างไฟล์ `Header.jsx`

```jsx
function Header({ title }) {
  return (
    <header className="site-header">
      <h1>{title}</h1>
    </header>
  )
}

export default Header
```

### ขั้นที่ 5 สร้าง Component PostCard

ไฟล์ `src/components/PostCard.jsx`

```jsx
function PostCard({ title, author, date }) {
  return (
    <article className="post-card">
      <h2>{title}</h2>
      <p>โดย {author} | {date}</p>
    </article>
  )
}

export default PostCard
```

### ขั้นที่ 6 สร้าง Component PostList

ไฟล์ `src/components/PostList.jsx` รับ `posts` แล้วใช้ `map` สร้าง PostCard ซ้ำ

```jsx
import PostCard from './PostCard'

function PostList({ posts }) {
  return (
    <section>
      {posts.map((post) => (
        <PostCard
          key={post.id}
          title={post.title}
          author={post.author}
          date={post.date}
        />
      ))}
    </section>
  )
}

export default PostList
```

### ขั้นที่ 7 ประกอบ Component ใน App.jsx

เพิ่มข้อมูลบทความอย่างน้อย 3 รายการ (ใส่ชื่อของตนเองเป็นผู้เขียน) แล้วส่งเป็น Props

```jsx
import Header from './components/Header'
import PostList from './components/PostList'

const posts = [
  { id: 1, title: 'เริ่มต้นกับ React', author: 'ชื่อของคุณ', date: '1 ธ.ค. 2569' },
  { id: 2, title: 'ใช้งาน Vite', author: 'ชื่อของคุณ', date: '8 ธ.ค. 2569' },
  { id: 3, title: 'เข้าใจ Props', author: 'ชื่อของคุณ', date: '15 ธ.ค. 2569' },
]

function App() {
  return (
    <>
      <Header title="My Blog" />
      <main>
        <PostList posts={posts} />
      </main>
    </>
  )
}

export default App
```

### ขั้นที่ 8 ตกแต่งด้วย CSS

ใส่ใน `src/index.css`

```css
body { font-family: sans-serif; margin: 0; background: #f5f5f5; }
main { max-width: 720px; margin: 0 auto; padding: 16px; }
.site-header { background: #8b1a1a; color: #fff; padding: 12px 16px; }
.post-card { background: #fff; border: 1px solid #ddd;
  border-radius: 8px; padding: 12px 16px; margin-bottom: 12px; }
```

### ขั้นที่ 9 ทดสอบการทำงาน

1. ตรวจว่าหน้าเว็บแสดงหัวเว็บและรายการบทความครบ 3 รายการ
2. กด `F12` เปิด Console แล้วตรวจว่าไม่มีข้อความสีแดง
3. ลองเพิ่มบทความรายการที่ 4 ในอาร์เรย์ `posts` แล้วดูว่าหน้าเว็บแสดงเพิ่มเอง โดยไม่ต้องแก้ Component
4. **ถ่ายภาพหน้าจอเป็นหลักฐานที่ 2**

### ขั้นที่ 10 ส่งงาน

1. กด `Ctrl+C` ใน Terminal เพื่อหยุด Dev Server
2. บีบอัดโฟลเดอร์ `blog-app` เป็น .zip โดย **ไม่รวม `node_modules`**
3. ส่งภาพหน้าจอ 2 ภาพ และไฟล์ .zip ตามช่องทางและเวลาที่ครูกำหนด

### ตอบคำถามท้ายใบงาน

1. สรุปสิ่งที่ได้เรียนรู้จากการปฏิบัติงาน
2. เหตุใดจึงควรแยกส่วนของหน้าเว็บเป็น Component ย่อย (ใช้ซ้ำได้ แก้ไขง่าย อ่านโค้ดง่าย)
3. Props ช่วยให้ Component ใช้งานซ้ำได้อย่างไร (ส่งข้อมูลต่างกันเข้าไป โดยใช้โครงสร้างเดิม)
4. ปัญหาที่พบและวิธีแก้ไข

### เกณฑ์คะแนน (เต็ม 5)

| รายการ | คะแนน |
|---|---|
| สร้างโปรเจกต์ด้วย Vite และรัน Dev Server แสดงผลได้ | 1 |
| แยก Component เป็นไฟล์ ชื่อขึ้นต้นตัวพิมพ์ใหญ่ import/export ถูกต้อง | 1 |
| ส่ง Props อย่างน้อย 3 ค่า และรับด้วย Destructuring | 1 |
| แสดงบทความอย่างน้อย 3 รายการด้วย `map` และ `key` | 1 |
| JSX ถูกต้อง ไม่มีข้อผิดพลาดใน Console และส่งตรงเวลา | 1 |

### ข้อควรระวัง

- ตั้งชื่อ Component ขึ้นต้นด้วยตัวพิมพ์ใหญ่ และให้ชื่อไฟล์ตรงกับชื่อ Component
- ใช้ `className` และมี Root Element เพียงตัวเดียว
- กด `Ctrl+S` ทุกครั้งก่อนดูผลในเบราว์เซอร์
- ห้ามแก้ไฟล์ใน `node_modules`

---

## 3. ใบกิจกรรมที่ 5: ทำงานกลุ่ม

**เป้าหมาย:** จำแนก SPA/MPA จับคู่ไฟล์กับหน้าที่ และแบ่ง Component ของหน้า Blog พร้อมกำหนด Props

**อุปกรณ์:** ใบกิจกรรม ใบความรู้ กระดาษ A4 ปากกาหรือปากกาเมจิก

### ขั้นที่ 1 จัดกลุ่มและแบ่งบทบาท (5 นาที)

1. แบ่งกลุ่ม กลุ่มละ 3-4 คน
2. เลือกบทบาท: หัวหน้ากลุ่ม ผู้บันทึก ผู้นำเสนอ ผู้ตรวจสอบเวลา
3. เขียนชื่อสมาชิกและกลุ่มที่ด้านบนใบกิจกรรม

### ขั้นที่ 2 กิจกรรมที่ 1 จำแนก SPA และ MPA (10 นาที)

อ่านข้อความแต่ละข้อ แล้วเขียน "SPA" หรือ "MPA"

เคล็ดลับ: ถ้าพูดถึงการโหลดหน้าใหม่ HTML สำเร็จรูป หรือ SEO ง่าย คือ **MPA** ถ้าพูดถึง JavaScript อัปเดตเฉพาะส่วน ดึง JSON จาก API หรือ `index.html` หน้าเดียว คือ **SPA**

### ขั้นที่ 3 กิจกรรมที่ 2 โครงสร้างโปรเจกต์ Vite (10 นาที)

จับคู่ไฟล์กับหน้าที่ แล้วเขียนตัวอักษรหน้าข้อความ ก-ฉ ลงในช่องคำตอบ

- `index.html` คือไฟล์ HTML หน้าเดียวที่มี `<div id="root">`
- `src/main.jsx` คือจุดเริ่มต้นที่นำ App ไปแสดงใน `#root`
- `src/App.jsx` คือ Component หลักที่ประกอบ Component อื่น
- `package.json` คือรายการ Dependencies และ scripts
- `vite.config.js` คือไฟล์ตั้งค่าของ Vite
- `node_modules/` คือแพ็กเกจที่ติดตั้งด้วย `npm install`

### ขั้นที่ 4 กิจกรรมที่ 3 แบ่ง Component ของหน้า Blog (25 นาที)

หน้า Blog ประกอบด้วย ส่วนหัวเว็บ (ชื่อเว็บและเมนู), รายการบทความ 3 รายการ (รูป ชื่อเรื่อง ผู้เขียน วันที่ ข้อความย่อ), แถบด้านข้างแสดงหมวดหมู่ 3 หมวด และส่วนท้ายเว็บ

**3.1 วาด Component Tree บนกระดาษ A4**

1. เขียน `App` ไว้บนสุด
2. ไล่หาส่วนของหน้าจอทีละส่วน แล้วตั้งเป็น Component ลูกของ App
3. ส่วนที่ซ้ำกัน (บทความ หมวดหมู่) ให้แยก Component ย่อยอีกชั้น

**3.2 สรุปลงตาราง** ระบุชื่อ Component (PascalCase) หน้าที่ และ Props

**3.3 ตรวจสอบ** ว่ารายการที่ซ้ำกันใช้ Component เดียว แล้วรับข้อมูลต่างกันผ่าน Props

### ขั้นที่ 5 นำเสนอและแลกเปลี่ยน (10 นาที)

ผู้นำเสนอแสดง Component Tree กลุ่มละไม่เกิน 2 นาที ฟังข้อเสนอแนะจากเพื่อนและครู

### ตอบคำถามสรุปและอภิปราย

1. SPA ต่างจาก MPA อย่างไร และ Blog App เหมาะกับแบบใดเพราะเหตุใด
2. เหตุใด Component จึงควรรับข้อมูลผ่าน Props แทนการเขียนข้อความตายตัว
3. ปัญหาหรือข้อโต้แย้งที่กลุ่มพบในการแบ่ง Component และข้อสรุปของกลุ่ม

### เกณฑ์คะแนน (เต็ม 10)

| รายการ | คะแนน |
|---|---|
| กิจกรรมที่ 1 จำแนก SPA/MPA | 2 |
| กิจกรรมที่ 2 จับคู่ไฟล์และหน้าที่ | 2 |
| กิจกรรมที่ 3 Component Tree และตาราง Props | 3 |
| การนำเสนอและตอบข้อซักถาม | 1 |
| สรุปและอภิปราย | 1 |
| ความร่วมมือและความรับผิดชอบ | 1 |

---

## 4. ใบมอบหมายงานที่ 5: โปรเจกต์ my-blog

**เป้าหมาย:** ต่อยอดจากใบงานที่ 4 สร้างหน้า Blog Home ตามหัวข้อที่สนใจ (อาหาร ท่องเที่ยว เกม เทคโนโลยี)

**ต้องส่ง:** ไฟล์ .zip ของ `my-blog` (ไม่รวม `node_modules`), ภาพหน้าจอผลลัพธ์ 1 ภาพ, ภาพ Console (F12) ที่ไม่มีข้อผิดพลาด 1 ภาพ

**กำหนดส่ง:** คาบเรียนถัดไป (สอนครั้งที่ 6) ส่งช้าจะถูกหักคะแนน

### ข้อกำหนดที่ต้องครบ

- [ ] สร้างด้วย Vite (React + JavaScript) ชื่อโปรเจกต์ `my-blog`
- [ ] มี Component อย่างน้อย 5 ตัว: Header, PostList, PostCard, Sidebar, Footer แยกไฟล์ใน `src/components` (เพิ่ม CategoryItem ได้)
- [ ] มีบทความอย่างน้อย 5 รายการ และหมวดหมู่อย่างน้อย 3 หมวด เก็บเป็นอาร์เรย์ใน `App.jsx` ด้วยข้อมูลของตนเอง
- [ ] ส่งข้อมูลด้วย Props เท่านั้น ห้ามเขียนข้อความบทความตายตัวใน PostCard และแสดงรายการด้วย `map` พร้อม `key`
- [ ] ใช้ `props.children` หรือ Default Parameter อย่างน้อย 1 จุด
- [ ] ตกแต่งด้วย CSS ให้อ่านง่ายและเป็นระเบียบ
- [ ] มี `README.md` ระบุชื่อ-สกุล วิธีรันโปรเจกต์ และ Component Tree สั้น ๆ

### ขั้นตอนทำงาน 7 ขั้น

**ขั้นที่ 1 วางแผนก่อนลงมือ**

ร่าง Component Tree บนกระดาษ พร้อมระบุ Props ของแต่ละตัว ตัวอย่าง

```text
App
├── Header        (siteName)
├── PostList      (posts)
│   └── PostCard  (title, author, date, summary, category)
├── Sidebar       (categories)
│   └── CategoryItem (name)
└── Footer        (text)
```

**ขั้นที่ 2 สร้างโปรเจกต์และล้างโค้ดเริ่มต้น**

```bash
npm create vite@latest my-blog -- --template react
cd my-blog
npm install
npm run dev
```

จากนั้นล้างโค้ดใน `App.jsx` และ `App.css` เหมือนขั้นที่ 3 ของใบงานที่ 4

**ขั้นที่ 3 เตรียมข้อมูลใน App.jsx**

```jsx
const posts = [
  { id: 1, title: '...', author: '...', date: '...', summary: '...', category: '...' },
  // เพิ่มให้ครบอย่างน้อย 5 รายการ
]

const categories = ['หมวดที่ 1', 'หมวดที่ 2', 'หมวดที่ 3']
```

**ขั้นที่ 4 สร้าง Component ทีละตัวและทดสอบทีละตัว**

เริ่มจาก PostCard แล้วจึงทำ PostList, Header, Sidebar และ Footer ตัวอย่างโครงของ Component ที่ยังไม่มีในใบงานที่ 4

```jsx
// src/components/PostCard.jsx  (เพิ่ม summary และ category)
function PostCard({ title, author, date, summary, category }) {
  return (
    <article className="post-card">
      <h2>{title}</h2>
      <p>โดย {author} | {date} | {category}</p>
      <p>{summary}</p>
    </article>
  )
}
export default PostCard
```

```jsx
// src/components/Sidebar.jsx  (ใช้ map + key และ Default Parameter)
function Sidebar({ title = 'หมวดหมู่', categories }) {
  return (
    <aside className="sidebar">
      <h3>{title}</h3>
      <ul>
        {categories.map((name) => (
          <li key={name}>{name}</li>
        ))}
      </ul>
    </aside>
  )
}
export default Sidebar
```

```jsx
// src/components/Footer.jsx  (ใช้ props.children ก็ได้ ตามข้อ 5.5)
function Footer({ children }) {
  return <footer className="site-footer">{children}</footer>
}
export default Footer

// เรียกใช้ใน App.jsx
// <Footer>© 2569 My Blog โดย ชื่อของคุณ</Footer>
```

**ขั้นที่ 5 ประกอบ Component ใน App.jsx แล้วตกแต่งด้วย CSS**

จัดโครงให้ตรงกับแบบในภาพที่ 1 ของใบมอบหมายงาน (ปรับตำแหน่งได้ แต่ต้องมี Component ครบ) เช่น ใช้ `display: flex` แบ่งรายการบทความกับ Sidebar เป็นสองคอลัมน์

#### เฉลยขั้นที่ 5 (ตัวอย่างคำตอบ ยอมรับคำตอบอื่นที่สมเหตุสมผล)

เนื้อหาบทความและหมวดหมู่ด้านล่างเป็นตัวอย่างหัวข้อเทคโนโลยี ให้เปลี่ยนเป็นข้อมูลและชื่อของตนเอง

**`src/components/Header.jsx`**

```jsx
function Header({ siteName }) {
  return (
    <header className="site-header">
      <h1>{siteName}</h1>
      <nav>
        <a href="#">หน้าแรก</a>
        <a href="#">เกี่ยวกับ</a>
        <a href="#">ติดต่อ</a>
      </nav>
    </header>
  )
}

export default Header
```

**`src/components/PostList.jsx`**

```jsx
import PostCard from './PostCard'

function PostList({ posts }) {
  return (
    <section className="post-list">
      {posts.map((post) => (
        <PostCard
          key={post.id}
          title={post.title}
          author={post.author}
          date={post.date}
          summary={post.summary}
          category={post.category}
        />
      ))}
    </section>
  )
}

export default PostList
```

**`src/App.jsx`**

```jsx
import Header from './components/Header'
import PostList from './components/PostList'
import Sidebar from './components/Sidebar'
import Footer from './components/Footer'

const posts = [
  { id: 1, title: 'เริ่มต้นกับ React', author: 'ชื่อของคุณ', date: '1 ธ.ค. 2569',
    summary: 'รู้จัก React และการแบ่งหน้าจอเป็น Component', category: 'React' },
  { id: 2, title: 'ใช้งาน Vite', author: 'ชื่อของคุณ', date: '8 ธ.ค. 2569',
    summary: 'สร้างโปรเจกต์ React ได้เร็วด้วย Vite', category: 'เครื่องมือ' },
  { id: 3, title: 'เข้าใจ Props', author: 'ชื่อของคุณ', date: '15 ธ.ค. 2569',
    summary: 'ส่งข้อมูลจาก Component แม่ไปยัง Component ลูก', category: 'React' },
  { id: 4, title: 'เขียน JSX ให้ถูกต้อง', author: 'ชื่อของคุณ', date: '22 ธ.ค. 2569',
    summary: 'สรุป 4 กฎของ JSX ที่ต้องจำ', category: 'JavaScript' },
  { id: 5, title: 'แสดงรายการด้วย map', author: 'ชื่อของคุณ', date: '29 ธ.ค. 2569',
    summary: 'ใช้ map และ key แสดงรายการซ้ำ', category: 'JavaScript' },
]

const categories = ['React', 'JavaScript', 'เครื่องมือ']

function App() {
  return (
    <>
      <Header siteName="My Blog" />
      <div className="layout">
        <main>
          <PostList posts={posts} />
        </main>
        <Sidebar categories={categories} />
      </div>
      <Footer>© 2569 My Blog โดย ชื่อของคุณ</Footer>
    </>
  )
}

export default App
```

**`src/index.css`**

```css
* { box-sizing: border-box; }

body {
  font-family: sans-serif;
  margin: 0;
  background: #f5f5f5;
  color: #222;
}

.site-header {
  background: #8b1a1a;
  color: #fff;
  padding: 12px 16px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.site-header h1 { margin: 0; font-size: 1.5rem; }
.site-header nav a { color: #fff; margin-left: 16px; text-decoration: none; }

.layout {
  max-width: 960px;
  margin: 0 auto;
  padding: 16px;
  display: flex;
  gap: 16px;
  align-items: flex-start;
}
.layout main { flex: 1; }

.post-card {
  background: #fff;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 12px 16px;
  margin-bottom: 12px;
}
.post-card h2 { margin: 0 0 4px; font-size: 1.2rem; }

.sidebar {
  width: 220px;
  background: #fff;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 12px 16px;
}
.sidebar h3 { margin-top: 0; }
.sidebar ul { margin: 0; padding-left: 20px; }

.site-footer {
  text-align: center;
  padding: 16px;
  background: #8b1a1a;
  color: #fff;
}
```

**จุดที่ใช้ตรวจให้คะแนน**

- ใช้ `<>` (Fragment) ห่อ Component ทั้งหมดใน `App` จึงมี Root Element เดียว
- ส่ง `posts` และ `categories` ให้ Component ลูกผ่าน Props เท่านั้น ไม่มีข้อความบทความตายตัวใน PostCard
- ใช้ `map` พร้อม `key` ทั้งใน PostList (`post.id`) และ Sidebar (`name`)
- ใช้ Default Parameter ใน Sidebar (`title = 'หมวดหมู่'`) และ `children` ใน Footer ครบตามข้อ 5.5
- เลย์เอาต์สองคอลัมน์ใช้ `display: flex` ใน `.layout` ถ้าไม่เห็นผล ให้ตรวจว่า `className` ใน `App.jsx` ตรงกับชื่อคลาสใน CSS

**ขั้นที่ 6 ตรวจสอบ Console**

กด `F12` อ่านข้อความผิดพลาดแล้วแก้ทีละจุด ข้อผิดพลาดที่พบบ่อย ได้แก่ ลืม `import`/`export` ลืม `key` ใช้ `class` แทน `className` และตั้งชื่อ Component ขึ้นต้นตัวพิมพ์เล็ก

**ขั้นที่ 7 เขียน README แล้วส่งงาน**

1. เขียน `README.md` ให้มีชื่อ-สกุล วิธีรันโปรเจกต์ (`npm install` แล้ว `npm run dev`) และ Component Tree สั้น ๆ
2. ถ่ายภาพหน้าจอผลลัพธ์ 1 ภาพ และภาพ Console ที่ไม่มีข้อผิดพลาด 1 ภาพ
3. บีบอัดโฟลเดอร์ `my-blog` เป็น .zip โดยไม่รวม `node_modules`
4. ส่งตามช่องทางที่ครูกำหนด

> ทำงานด้วยตนเอง อ่านใบความรู้และเอกสารอ้างอิงได้ แต่ห้ามคัดลอกงานของผู้อื่น และต้องอธิบายโค้ดของตนเองได้เมื่อครูซักถาม

### เกณฑ์คะแนน (เต็ม 5)

| รายการ | คะแนน |
|---|---|
| สร้างด้วย Vite และมี Component อย่างน้อย 5 ตัว แยกไฟล์ถูกต้อง | 1 |
| ส่งข้อมูลด้วย Props ถูกต้อง แสดงรายการด้วย `map` และ `key` | 1 |
| มีบทความอย่างน้อย 5 รายการและหมวดหมู่แสดงครบ | 1 |
| หน้าเว็บเรียบร้อย มี CSS, README และไม่มีข้อผิดพลาดใน Console | 1 |
| ส่งตรงเวลาและอธิบายโค้ดของตนเองได้ | 1 |

---

## 5. สรุปคำสั่งที่ใช้บ่อย

| คำสั่ง | หน้าที่ |
|---|---|
| `npm create vite@latest ชื่อโปรเจกต์ -- --template react` | สร้างโปรเจกต์ React ด้วย Vite |
| `npm install` | ติดตั้งแพ็กเกจที่โปรเจกต์ใช้ |
| `npm run dev` | รัน Development Server (หยุดด้วย `Ctrl+C`) |
| `npm run build` | สร้างไฟล์สำหรับนำขึ้นใช้งานจริง (โฟลเดอร์ `dist`) |
| `npm run preview` | ทดลองดูผลลัพธ์ของไฟล์ที่ build แล้ว |

## 6. แหล่งค้นคว้าเพิ่มเติม

- React Documentation: https://react.dev/learn
- Vite Getting Started: https://vite.dev/guide/
- MDN Web Docs: https://developer.mozilla.org/
