# demo
https://user-images.githubusercontent.com/7900087/115066217-10e1f100-9ea4-11eb-8242-c90bfdeb1678.mp4


```json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```


```rb
require_relative "helper"

 module GetUsersUserNameSharedTests
   def test_get_user
     authenticate_as @owner, organization: @org

     data = api :get, "/users/#{@owner}"
     assert_equal 200, last_response.status
     assert_match "/users/#{@owner}", data["url"]
     assert_schema :v3, :private_user, data
   end

   def test_email_field_is_not_nil_when_authed
     unless @owner.is_enterprise_managed?
       verified_email = create(:user_email, :verified, user: @owner).email
       @owner.profile_email = verified_email
       @owner.save!
     end

     authenticate_as @owner, organization: @org

     data = api :get, "/users/#{@owner}"
     assert_schema :v3, :private_user, data
     refute_nil data["email"]
   end
 end
 ```
