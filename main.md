### create address table with id and address as char.

```
CREATE TABLE public.address (
	id uuid NOT NULL DEFAULT uuid_generate_v4(),
	"data" varchar NOT NULL,
	CONSTRAINT address_pk PRIMARY KEY (id)
);
ALTER TABLE public.address ADD CONSTRAINT address_fk FOREIGN KEY (id) REFERENCES public."user"(id) ON DELETE CASCADE ON UPDATE CASCADE;


```

### create category table with product id nad category name

```
CREATE TABLE public.category (
	id uuid NOT NULL,
	category_id uuid NOT NULL,
	uuid uuid NOT NULL DEFAULT uuid_generate_v4()
);
CREATE INDEX category_c_name_idx ON public.category USING btree (category_id);
ALTER TABLE public.category ADD CONSTRAINT category_fk_2 FOREIGN KEY (category_id) REFERENCES category_product(id);



```

### category_product joint table

```
CREATE TABLE public.category_product (
	product_id uuid NOT NULL DEFAULT uuid_generate_v4(),
	category_name varchar NOT NULL,
	id uuid NOT NULL DEFAULT uuid_generate_v4(),
	CONSTRAINT category_product_pk PRIMARY KEY (id),
	CONSTRAINT category_product_un UNIQUE (category_name)
);
ALTER TABLE public.catrgory_product ADD CONSTRAINT product_catrgory_fk_2 FOREIGN KEY (product_id) REFERENCES product(id);


```

### Create order table with user and address details with price

```
-- public."order" definition

-- Drop table

-- DROP TABLE public."order";

CREATE TABLE public."order" (
	user_id uuid NOT NULL,
	address_id uuid NOT NULL,
	order_id uuid NOT NULL DEFAULT uuid_generate_v4(),
	price varchar NOT NULL,
	CONSTRAINT orders_pk PRIMARY KEY (order_id)
);
ALTER TABLE public.order ADD CONSTRAINT order_fk FOREIGN KEY (address_id) REFERENCES "address"(id) ON UPDATE CASCADE ON DELETE CASCADE;


```
### product table with product price name and description

```
-- public.product definition

-- Drop table

-- DROP TABLE public.product;

CREATE TABLE public.product (
	"name" varchar NOT NULL,
	description varchar NOT NULL,
	price varchar NOT NULL,
	sku uuid NOT NULL DEFAULT uuid_generate_v4(),
	CONSTRAINT products_pk PRIMARY KEY (sku)
);

CREATE INDEX products_name_idx ON public.product USING btree (name);4
```
### product order joint table 

```
CREATE TABLE public."order" (
	user_id uuid NOT NULL,
	address_id uuid NOT NULL,
	order_id uuid NOT NULL DEFAULT uuid_generate_v4(),
	price float8 NOT NULL,
	CONSTRAINT orders_pk PRIMARY KEY (order_id)
);
ALTER TABLE public.order_product ADD CONSTRAINT product_order_fk FOREIGN KEY (order_id) REFERENCES "order"(order_id);
ALTER TABLE public.order_product ADD CONSTRAINT product_order_fk_2 FOREIGN KEY (product_id) REFERENCES product(id);


```
### Creating User table
```
CREATE TABLE public."user" (
	"name" varchar NOT NULL,
	address_id varchar NOT NULL,
	phone varchar NOT NULL,
	email varchar NOT NULL,
	passord varchar NOT NULL,
	id uuid NOT NULL DEFAULT uuid_generate_v4(),
	CONSTRAINT user_pk PRIMARY KEY (id)
);
```
### Insertion

```

INSERT INTO public.address (id,"data") VALUES
	 ('dc1b0cc5-6647-4a1a-acc3-4f122d452b8c','123 house'),
	 ('b5b8891b-a695-48e0-89aa-50ab300ef962','456 house'),
	 ('edf84548-92f1-4aff-adb0-6f3ce4748bca','789 house');

INSERT INTO public.category (id,category_id,uuid) VALUES
	 ('70cde5c5-7ccf-4406-bc7f-df36cc1a0916','2f8dd342-6401-4f37-aef6-da9bfeb08d53','def2cd71-708b-4dce-8a7b-e9c46ac21311'),
	 ('38b3b8d5-5aa8-4389-8679-caed3ddcff55','f22e8df4-4308-40a5-aaad-85c087f1d553','87572274-5b15-4ce7-85fc-0f788537ab4e'),
	 ('38b3b8d5-5aa8-4389-8679-caed3ddcff55','2f8dd342-6401-4f37-aef6-da9bfeb08d53','bf7c7bda-0c84-4b65-bad0-66c75020d1ab'),
	 ('7c8406c9-8616-462e-8910-b6eb1187d45d','2f8dd342-6401-4f37-aef6-da9bfeb08d53','480c2b39-5e60-475c-b3b7-fe939b11b4c0'),
	 ('7c8406c9-8616-462e-8910-b6eb1187d45d','f22e8df4-4308-40a5-aaad-85c087f1d553','56c252db-fb1c-44b2-b212-2c836f46cc60'),
	 ('7e532e3b-8515-40bf-abaf-401cb44fb983','2f8dd342-6401-4f37-aef6-da9bfeb08d53','28bcbc3d-1a28-4862-9d37-b1addd791960'),
	 ('e2733635-3ef8-48ce-b2ab-35518791f932','a380e4b8-5bbf-437c-98ce-4bb54207d1c5','acace5e1-5c05-451e-8e8e-6b1203b3d5a2');

INSERT INTO public.category_product (product_id,category_name,id) VALUES
	 ('2f8dd342-6401-4f37-aef6-da9bfeb08d53','electronics','5726b66c-8210-4e1f-ba57-69ba178ba387'),
	 ('f22e8df4-4308-40a5-aaad-85c087f1d553','lightings','9f984bf9-49c9-4a89-890a-25b134bb2c4e'),
	 ('a380e4b8-5bbf-437c-98ce-4bb54207d1c5','food','2bf3e4f5-f74d-4835-ac50-c7cc544c6e06');
INSERT INTO public."order" (user_id,address_id,order_id,price) VALUES
	 ('dc1b0cc5-6647-4a1a-acc3-4f122d452b8c','d8fc9b9e-91b2-4cdd-a32a-d557de70ffba','40757862-3392-4466-8844-098980cb3390',110.0),
	 ('b5b8891b-a695-48e0-89aa-50ab300ef962','fee3bbdf-9071-4351-b29d-3db4bb1e8865','d0441618-88ad-478d-a6bd-3a0d0b7e2098',50.0),
	 ('dc1b0cc5-6647-4a1a-acc3-4f122d452b8c','d8fc9b9e-91b2-4cdd-a32a-d557de70ffba','88e06132-e09c-4435-89ab-ac2f47651c5e',200.0),
	 ('edf84548-92f1-4aff-adb0-6f3ce4748bca','871266f9-a68c-4e03-81e0-5ffd2a1da1cf','2eac2736-5da2-4010-8bff-231b0c9d93c6',10.0),
	 ('edf84548-92f1-4aff-adb0-6f3ce4748bca','871266f9-a68c-4e03-81e0-5ffd2a1da1cf','7967eada-7ad4-4eae-ad61-46dea11f62dd',20.0);

INSERT INTO public.order_product (order_id,product_id,count,tot_price) VALUES
	 ('40757862-3392-4466-8844-098980cb3390','70cde5c5-7ccf-4406-bc7f-df36cc1a0916',1,100.0),
	 ('40757862-3392-4466-8844-098980cb3390','e2733635-3ef8-48ce-b2ab-35518791f932',2,10.0),
	 ('d0441618-88ad-478d-a6bd-3a0d0b7e2098','38b3b8d5-5aa8-4389-8679-caed3ddcff55',1,20.0),
	 ('d0441618-88ad-478d-a6bd-3a0d0b7e2098','7e532e3b-8515-40bf-abaf-401cb44fb983',1,30.0),
	 ('88e06132-e09c-4435-89ab-ac2f47651c5e','70cde5c5-7ccf-4406-bc7f-df36cc1a0916',2,200.0),
	 ('2eac2736-5da2-4010-8bff-231b0c9d93c6','e2733635-3ef8-48ce-b2ab-35518791f932',2,10.0),
	 ('7967eada-7ad4-4eae-ad61-46dea11f62dd','38b3b8d5-5aa8-4389-8679-caed3ddcff55',1,20.0);
INSERT INTO public.product ("name",description,price,id,sku) VALUES
	 ('laptop','msi uyir','100','70cde5c5-7ccf-4406-bc7f-df36cc1a0916','28fd5f86-ff1e-43cd-b057-9497354c217c'),
	 ('mouse','hp thanne','20','38b3b8d5-5aa8-4389-8679-caed3ddcff55','e26b45b1-faff-4809-8fbd-6efc7cad0371'),
	 ('keyboard','minni kathum','40','7c8406c9-8616-462e-8910-b6eb1187d45d','4e39d5f4-09b2-4a41-8d6d-8b30d37236ef'),
	 ('fan','nalla thanuppundu','30','7e532e3b-8515-40bf-abaf-401cb44fb983','666ab624-9ac8-4159-b5fa-0478f82305de'),
	 ('motta','viriyoolla','5','e2733635-3ef8-48ce-b2ab-35518791f932','6c66fb9f-428b-461a-88a4-4f70948cbe3f');

INSERT INTO public."user" ("name",address_id,phone,email,passord,id) VALUES
	 ('Kiran','d8fc9b9e-91b2-4cdd-a32a-d557de70ffba','9495342342','suku@suku.com','pass','dc1b0cc5-6647-4a1a-acc3-4f122d452b8c'),
	 ('Vidya','fee3bbdf-9071-4351-b29d-3db4bb1e8865','9494222222','vidya@suku.com','pass','b5b8891b-a695-48e0-89aa-50ab300ef962'),
	 ('Vaishnav','871266f9-a68c-4e03-81e0-5ffd2a1da1cf','94922342342','vaishnav@suku.com','pass','edf84548-92f1-4aff-adb0-6f3ce4748bca');

```

