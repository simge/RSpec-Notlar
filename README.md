## RSpec Nedir ?

RSpec, Ruby için yazılmış bir test frameworküdür. RSpec, kodumuzun doğru ve beklenilen şekilde çalıştığından emin olmak için kullanabileceğimiz bir araçtır. RSpec, testleri yazarken okunaklı ve anlaşılır hale getirmek için BDD (Behavior Driven Development - Davranış Odaklı Geliştirme) yöntemini kullanır. Bu yöntem, kodun nasıl davranması gerektiğini ve ne yapması gerektiğini açık bir şekilde tanımlar. RSpec, Ruby dili için yazılmıştır ve Rails uygulamalarının testlerini yazmak için popülerdir.

## İÇİNDEKİLER

* [Describe kullanımı](#describe-kullanımı)
* [Context kullanımı](#context-kullanımı)
* [It kullanımı](#it-kullanımı)
* [Expect kullanımı](#expect-kullanımı)
* [Let kullanımı](#let-kullanımı)
* [RSpec çıktı formatları](#rspec-çıktı-formatları)
* [Kaynaklar](#kaynaklar)




## Describe kullanımı

RSpec tarafından test edilen sınıf veya metodun tanımını yapar. 
```ruby
describe HelloWorld do
.
.
.
end
```
Best practice kullanım için class methodlarının test edilmesinde uzun uzun açıklama yazmak yerine "." ön eki kullanılırken, instance methodların test edilmesinde "#" ön eki kullanılmalıdır.

```ruby
# wrong
describe "the authenticate method for User" do
describe "the save method for User" do

# correct
describe ".authenticate" do
describe "#save" do
```

## Context kullanımı

Testlerin daha rahat okunabilirliği için bir alt kategori oluşturur. Örnek olarak, `context 'when user is admin'` kullanılırsa, sadece admin olan kullanıcılar için testler yapılmaktadır.

```ruby
# wrong
describe User do
  it "should save when name is not empty" do
    ...
  end
  it "should not save when name is empty" do
    ...
  end

  it "should not be valid when name is empty" do
	  ...
  end
  it "should be valid when name is not empty" do
    
  end
end

# correct
describe User do

  context "when name is empty" do
    it "should not be valid" do
     ...
    end
    it "should not save" do
      ...
    end
  end

  context "when name is not empty" do
    
    it "should be valid" do
      ...
    end
    it "should save" do
      ...
    end
  end
end
```

## It kullanımı

Testlerin tanımını yapar. Örnek olarak, `it 'should be valid'` kullanımı, test edilen sınıfın geçerli olup olmadığını test etmektedir.

```ruby
describe User do
  context "when name is empty" do
    it "should not be valid" do
     ...
    end
    it "should not save" do
      ...
    end
  end
end
```

## Expect kullanımı

Testin beklentisini tanımlar. Örnek olarak, `expect(user.admin?).to be true` kullanılırsa, kullanıcının admin olduğunun doğruluğu test edilmektedir.

```ruby
describe "Number" do
  it "should be positive" do
    number = 5
    expect(number).to be > 0
  end
end
```
Bu test, sayının 0'dan büyük olmasını bekler ve eğer sayı 0'dan büyükse test başarılı olarak sonuçlandırılır. Aksi halde, test başarısız olarak sonuçlandırılır.

`to ve be ` testin beklentisini tanımlayan expect metodunun bir parçasıdır.

## Let kullanımı

`let` metodunu kullanarak testlerimizde yinelenen kodu azaltabiliriz. `let` metodu, belirli bir değişkeni tanımlayarak veya bir bloğu çalıştırarak o değişkenin değerini oluşturur. Bu değişken, daha sonra herhangi bir testte kullanılabilir. Örneğin, aşağıdaki testlerde `user` değişkenini kullanabiliriz:

```ruby
describe "User" do
  let(:user) { User.new(name: "John", age: 30) }

  it "has a name" do
    expect(user.name).to eq("John")
  end

  it "has an age" do
    expect(user.age).to eq(30)
  end
end
```

## RSpec çıktı formatları

Varsayılan RSpec çıktısı "progress" biçimindedir. RSpec çıktı formatlarında `progress, documentation, json ve html` çıktılarını görebiliriz.

Bunun için testi çalıştırırken ;


```ruby
rspec foo.spec -f d 	# documentation formatında testin çıktılarını gösterir.
rspec foo.spec -f j 	# json formatında testin çıktılarını gösterir.
rspec foo.spec -f h     # html formatında testin çıktılarını gösterir.
```

## Kaynaklar

* [ChatGPT](https://chat.openai.com)
* [RSpec Best Practices](https://github.com/abinoda/rspec-best-practices/edit/master/readme.md)
* [RSpec Tutorial](https://www.rubyguides.com/2018/07/rspec-tutorial/)




