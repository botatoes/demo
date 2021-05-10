# demo



```
We just added a copy button to all code blocks

Happy Monday
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
