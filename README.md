# JobPlacementPortfolio
Live Project 
## Introduction
For the last two weeks of my time at the tech Academy, I got to worked with my peers to build an app for local Theatre in Portland; MVC/MVVM Web Application in C#, Lambda expressions, JQuery Ajax and ASP.NET were required. It was a great learning opportunity for fixing other peers' code, Adding things to the App. The biggest problem was time we did not have enough time to be able to work on that project, but we used what we had to deliver what was needed on time. During that time I saw how good developers work with what they have to make a quality product. I worked on several back end stories that I am very proud of. Everyone on the team had a chance to work on front end and [back end stories](#back-end-stories). Over the two weeks sprint I learned a lot and gained a lot of [skills](#other-skills-learned) that I'm confident I will use again and again on future projects. 

Below are descriptions of the stories I worked on, along with code snippets.I also have some full code files in this repo for the larger functionalities I implemented.


## Back End Stories
* [Editing MVC Controler](#editing-mvc-controler)
* [Creating Link](#creating-link)


## Editing MVC Controler
Adding delete link that allow admin to delete user input.

    [HttpPost, ActionName("Delete")]
        public ActionResult DeleteMember(string Id)
        {
            bool result = false;
            ApplicationUser s = db.Users.Where(x => x.Id == Id).SingleOrDefault();
            if (s != null)
            {
                ApplicationUser user = db.Users.Find(Id);
                //s.isDeleted = true;
                db.Users.Remove(user);
                db.SaveChanges();
                result = true;
            }
            // return Json(result, JsonRequestBehavior.AllowGet);
            return RedirectToAction("UserList");
        }
        //adding subscribe link that allow admin to delete user input
        [HttpPost, ActionName("Subscribers")]
        public ActionResult DeleteSubscribers(string Id)
        {
            bool result = false;
            ApplicationUser s = db.Users.Where(x => x.Id == Id).SingleOrDefault();
            if (s != null)
            {
                ApplicationUser user = db.Users.Find(Id);
                db.Users.Remove(user);
                db.SaveChanges();
                result = true;
            }
            // return Json(result, JsonRequestBehavior.AllowGet);
            return RedirectToAction("UserList");
        }
 
## Creating-link
In this story my task was to create a link that can Allow the Admin to delete database that the Users entered. 
I have to create a Delete Confirmation pop up windows(modal)that ask the Admin if they want to delete data.

    @if (item.Role == "Subscriber")
        {
          <a href="@Url.Action("Details", "Subscriber", new { id = item.SubscriberPerson.SubscriberId, area = "Subscribers" }, null)">Details </a> @:|
          <a href="@Url.Action("Edit", "Subscriber", new { id = item.SubscriberPerson.SubscriberId, area="Subscribers"}, null)"> Edit </a>@:|
          <a href="@Url.Action("DeleteSubscribers", "Admin", new { id = item.SubscriberPerson.SubscriberId}, null)" data-toggle="modal" data-target="#myModal" data-element-to-             delete="item.SubscribersID"> Delete </a><br>
        }
        @if (item.Role == "Member")
        {
       @Html.ActionLink("Details", "Details", "CastMember", new { id = item.CastMemberUserID }, null) this was the way the link for CastMember Details was previously                       implemented@
          <a href="@Url.Action("Details", "CastMembers", new { id = item.CastMemberUserID}, null)">Details </a>@:|
          <a href="@Url.Action("Edit", "CastMembers", new { id = item.CastMemberUserID}, null)"> Edit </a>@:|
          <a href="@Url.Action("DeleteConfirmed", "Admin", new { id = item.CastMemberUserID}, null)" data-toggle="modal" data-target="#myModal1" data-element-to- b                   delete="item.CastMemberUserID"> Delete </a><br>

          
Using Ajax and Javascrip 


  Creating a delete modal for member

<!-- Modal -->
          
          <div class="modal fade" id="myModal" role="dialog">
            <div class="modal-dialog">
               <!-- Modal content-->
              <div class="modal-content">
                <div class="modal-header">
                  <div class="modal fade" id="DeleteConfirmation">
                    <button type="button" class="close" data-dismiss="modal">&times;</button>
                    <h4 class="modal-title">Delete Member</h4>
                  </div>
                  <div class="modal-body">
                    <h4>Are you sure? You want to Delete this Record. </h4>
                  </div>
                  <div class="modal-footer">
                    <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
                    <a href="#" class="btn btn-primary" data-dismiss="modal">Cancel</a>
                    <button class="btn btn-danger" onclick="ConfirmDelete()">Confirm</button>
                  </div>
                </div>
              </div>
            </div>
          </div>
          //end of modal
          <script>
          function DeleteMember(Member) {
            $("#MemberId").val(Member);
            $("#DeleteConfirmation").modal("show");
          }
          function ConfirmDelete() {
            var MemberId = $("#MemberId").val();
            console.log("Delete");
            $.ajax({
              method: "POST",
              url: "@Url.Action("Delete","Admin")",
              data: { Id: "@item.Id" },
              success: function (result) {
                $("#DeleteConfirmation").modal("hide");
              // $(".row_" + Member).remove();
              }
            });

          </script>
       

* Jump to: [Back End Stories](#back-end-stories), [Other Skills](#other-skills-learned), [Page Top](#live-project)*
 

## Other Skills Learned
* Working with a group of developers to identify front and back end bugs to the improve usability of an application
* To be able to communicate with others developers on what need works
* Learning form other developers by observing their workflow and ask lot of questions

* Jump to: [Back End Stories](#back-end-stories), [Other Skills](#other-skills-learned), [Page Top](#live-project)*
