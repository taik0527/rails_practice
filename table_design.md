* Users
  * name: string
  * email: string
  * image: string
  * password_digest: string
  * id: int
  * admin: boolean

* Questions
  * title: string
  * body: text
  * created_at: datetime
  * updated_at: datetime
  * id: int
  * solved: boolean
  * user_id: int

* Answers
  * body: text
  * created_at: datetime
  * updated_at: datetime
  * user_id: int
  * question_id: int
