# MDiSUBD
Data base labs of 5th semester will be stored in this repository


1. Данные студента:
   * Шайкова Вероника Андреевна
   * 153502
   * магазин музыкальных товаров
  
2. Функциональные требования:
   * Предметная область
     - Предметной областью является музыкальный магазин. Здесь товары представляют собой различные носители музыки: диски, пластинки и т.п. У каждый товар характеризуется исполнителем, альбомом и категорией (другие поля указаны в описаниях сущности)
   * Авторизация пользователя
     - для авторизации необходимо указать ФИО, 
   * Возможность совершения покупки
     - такая возможность есть только у авторизованного пользователя
     - пользователь добавляет товар в корзину (только для авторизованных) с возможностью выбора количества товаров. После товар(-ы) из корзины можно выбрать для создания заказа
   * Удобная сортировка товаров
     - Сортировка товаром может осуществляться по категории, жанру и/или исполнителю.
   * Управление пользователями (CRUD)
   * Система ролей
     - администратор: управляет всеми сущностями для нормальной работы магазина (не может совершать заказы и добавлять товары в корзину)
     - незарегистрированный пользователь: только просмотр каталога и возможность создать аккаунт
     - зарегистрированый пользователь: возможность удалить профиль, модифицировать личную информацию, просмотр каталога, добавление товара в корзину, просмотр корзины, совершение заказа на основе товаров в корзине
   * Журналирование действий пользователя
   * Сбор данных для выявления рейтинга товаров определенного типа / исполнителя
     - для этого фиксируется количество проданных товаров, для каждого альбома или исполнителя
  
4. Сущности:
   1. Users (Пользователь)
      * Основная информация о зарегистрированных пользователях
        
      - u_id: Primary Key, Уникальный идентификатор пользователя
      - fio: ФИО пользователя
      - email: Адрес электронной почты пользователя (уникальный)
      - password: Пароль пользователя
      - login: Логин пользователя (Уникальный)
      - с_id: Foreign Key, указывает на карту, использующуюся для покупок в магазине
      - r_id: Foreign Key, указывает на роль пользователя в системе


   2. Roles (Роль)
      * Определяет роли, зоны доступа и ответственности пользователей

      - r_id: Primary Key, Уникальный идентификатор роли пользователей
      - r_name: Уникальное название роли
      - r_description: Описание роли


   3. Cards (Карта)
      * Данные о платежных картах пользователя, необходимые для оформления заказа

      - card_id: Primary Key, Уникальный идентификатор карты
      - card_number: 16-значный номер карты


   4. Products (Товар)
      * Основные данные о единицах продукции магазина

      - p_id: Primary Key, Уникальныq идентификатор наименования товара
      - al_id: Foreign Key, Указывает на альбом
      - ar_id: Foreign Key, Указывает на исполнителя
      - cat_id: Foreign Key, Категория товара
      - m_id: Foreign Key, Производитель товара
      - p_year: Год производства товара
      - p_name: Имя товара
      - p_description: Краткое описание товара
      - p_price: Цена на едтиницу товара


   5. Categories (Категория)
      * Категория товаров, с помощью которой можно отсортировать их и получить список       
        альтернативных товаров (кассеты/пластинки и т.п.)

      - cat_id: Primary Key, Уникальный идентификатор категории товара
      - cat_name: Название категории товара
       

   6. Genres (Жанр)
      * Жанр непосредственно музыкального товара/альбома/исполнителя
        
      - g_id: Primary Key, Уникальный идентификатор музыкального жанра
      - g_name: Название жанра
   
  

   7. Artists (Исполнитель)
      * Информация об исполнителе, рейтинг

      - ar_id: Primary Key, Уникальный идентификатор исполнителя
      - ar_name: Имя исполнителя/ Название группы
      - ar_solled: Количество проданных единиц товара данного исполнителя
      - ar_description: Краткая информация об исполнителе


   8. Albums (Альбом)
      * Информация об альбоме, рейтинг
     
      - al_id: Primary Key, Уникальный идентификатор альбома
      - al_name: Название альбома
      - al_year: Год выпуска альбома
      - ar_id: Foreign Key, Указывает на исполнителя, выпустившего альбом
      - al_solled: Количество проданных единиц товара с данным альбомом


   9. Manufacturers (Производитель)
      * Информация о произвоителе непоследственно товара
  
      - m_id: Primary Key, Уникальный идентификатор производителя
      - m_name: Название компании / ИП
      - m_adress: Юридический адрес производителя


   10. OrderedProducts (Товар в заказе)
      * Сущность для организации связи между товарами и заказами (в качестве посредника)
      
      - o_id: Primary Key, Указывает на связанный заказ
      - p_id: Primary Key, Указывает на связанный товар
      - op_ammount: количество единиц определенного товара в заказе
  
   11. ProductsCart (Товар в корзине)
      * Сущность для организации связи между товарами и заказами (в качестве посредника)
      
      - cart_id: Primary Key, Указывает на связанную корзину
      - p_id: Primary Key, Указывает на связанный товар
      - cartp_ammount: количество единиц определенного товара в корзине пользователя


   12. Orders (Заказ)
      * Данные о заказах, совершаемых пользователями магазина

      - o_id: Primary Key, Уникальный идентивикатор заказа
      - u_id: Foreign Key, Пользователь, совершивший заказ
      - o_datetime: время оформления заказа
      - o_del_status: статус сборки/доставки
      - o_pay_status: статус оплаты
      - o_adress: адрес доставки
      - o_total_cost: Полная стоимость заказа (все товары + доставка)
   

   13. Stock (Склад)
      * Перечеь имеющихся (и не имеющихся) в наличии товаров

      - s_id: Primary Key, Уникальный идентификатор единицы на складе
      - p_id: Foreign Key, Указывает на id товара, подсчет которого ведется
      - ammount: Количество оставшихся в наличии единиц конкретного товара


     14. Cart (Корзина)
      * Список товаров, которые пользователь хочет заказать и поместил в корзину
     
      - cart_id: Primary Key, Уникальный идентификатор корзины
      - u_id: Foreign Key, Пользователь, управляющий корзиной


4. Ограничения

   1. Users
      - u_id: int PK autoincrement
      - fio: varchar(100) not null
      - email: varchar(64) not null unique
      - cart_id: int Foreign Key
      - с_id: int Foreign Key
      - r_id: int Foreign Key
      - password: varchar(300) not null (в зашифрованном виде)
      - login: varchar(30) not null unique


   2. Roles 
      - r_id: int Primary Key autoincrement
      - r_name: varchar(20) unique not null
      - r_description: text


   3. Cards
      - card_id: int Primary Key autoincrement
      - card_number: varchar(16) not null


   4. Products 
      - p_id: int Primary Key autoincrement
      - al_id: int Foreign Key
      - ar_id: int Foreign Key
      - cat_id: int Foreign Key
      - m_id: int Foreign Key
      - p_year: int not null (>0)
      - p_name: varchar(100) not null
      - p_description: text
      - p_price: double not null (>0)


   5. Category 
      - cat_id: int Primary Key autoincrement
      - cat_name: varchar(20) not null
       

   6. Genre 
      - g_id: int Primary Key autoincrement
      - g_name: varchar(30) not null
   
  

   7. Artist
      - ar_id: int Primary Key autoincrement
      - ar_name: varchar(30) not null
      - ar_solled: int not null (>0)
      - ar_description: text


   8. Album 
      - al_id: int Primary Key autoincrement
      - al_name: varchar(30) not null
      - al_year: int not null (>0)
      - ar_id: int Foreign Key
      - al_solled: int not null (>=0)


   9. Manufacturers
      - m_id: int Primary Key autoincrement
      - m_name: varchar(30) not null
      - m_adress: text not null


   10. OrderedProducts (Composite PK)
      - o_id: int Primary Key
      - p_id: int Primary Key
      - op_ammount: int not null (>0)
  
   11. ProductsCart (Товар в корзине)
      - cart_id: int Primary Key
      - p_id: int Primary Key
      - cartp_ammount: int not null (>0)


   11. Orders
      - o_id: int Primary Key autoincrement
      - u_id: int Foreign Key
      - o_datetime: datetime not null
      - o_del_status: varchar(30) not null
      - o_pay_status: boolean not null
      - o_adress: text not null
      - o_total_cost: double not null (>0)
   

   12. Stock
      - s_id: int Primary Key autoincrement
      - p_id: int Foreign Key
      - ammount: int not null (>=0)

   14. Cart (Корзина)
      - cart_id: int Primary Key autoincrement
      - u_id: int Foreign Key


  2 Лабораторная (недосущности на будущее)

   7. AlbumGenre (Жанры альбома)
      * Промежуточная таблица из-за возможности мультижанрового альбома

      - al_id: Primary Key, Указывает на свзанный альбом
      - g_id: Primary Key, Указывает на связанный жанр
        

    8. ArtistGenre (Жанры производителя)
       * Промежуточная таблица из-за возможности работы исполнителя в нескольких жанрах

       - ar_id: Primary Key, Указывает на свзанного исполнителя
       - g_id: Primary Key, Указывает на связанный жанр

      7. AlbumGenre
      - al_id: Primary Key, Указывает на свзанный альбом
      - g_id: Primary Key, Указывает на связанный жанр
        

    9. ArtistGenre (Composite PK)
       - ar_id: int Primary Key
       - g_id: int Primary Key


   
