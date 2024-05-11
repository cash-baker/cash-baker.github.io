---
layout: project
type: project
image: img/clubhub-225.png
title: Item Depot Project
date: 2024
published: true
labels:
summary: "Web application to list and retrieve lost and found items at UH Manoa"
---
<img class="img-fluid" src="../img/club-list-page.png">

For our class project, my team of four and I developed 'Item Depot,' a website enhancing UH Manoa's in-person lost and found system. Users could sign up, submit item details, and receive automated email alerts for found items. Item Depot was built with Meteor, Node.js, MongoDB, and React.

Primarily, I handled programming tasks: creating item submission pages, writing item schemas, updating the GitHub homepage, and scheduling meetings. I also implemented features for editing entries and admin controls, along with TestCafe acceptance tests. Below is a snippet testing item addition and display
```
class AddLostItemPage {
  constructor() {
    this.pageId = '#add-lost-page';
    this.pageSelector = Selector(this.pageId);
  }

  /** Asserts that this page is currently displayed. */
  async isDisplayed(testController) {
    await testController.expect(this.pageSelector.exists).ok();
  }
  // Asserts that an item can be added and displayed
  async addLostItem(testController) {
    const lostItemTest = { itemName: 'Cinnamoroll', lastSeen: 'Hamilton Library', description: 'a silly lil guy' };
    await testController.typeText('#item-name-field', lostItemTest.itemName);
    
    // Testing image upload functionality
    await testController.setFilesToUpload('#file-input', '../public/images/meteor-logo.png');
    const categorySelect = Selector('#category-field');
    const categoryOption = categorySelect.find('option');
    await testController.click(categorySelect);
    await testController.click(categoryOption.withText('Miscellaneous'));
    await testController.typeText('#last-seen-field', lostItemTest.lastSeen);
    await testController.typeText('#description-field', lostItemTest.description);
    await testController.click('#submit-btn input.btn.btn-primary');
    await testController.click('.swal-button--confirm');
    
    // Check if newly created item is added to lost items page
    await navBar.gotoListLostItemPage(testController);
    await testController.click(Selector('.card-title').withText((lostItemTest.itemName)));
  }
}
```
My final task was creating a point system, which would automatically awarded users points for finding items, and a leaderboard to display the ranking of each user (snippet shown below)

````
const UserPointsItem = ({ user, rank }) => (
  <tr>
    <td>{rank}</td>
    <td>
      <img src={user.image} alt="Profile" id="lb-profile-pics" />
      <Link to={`/profile/${user._id}`}>{user.firstName} {user.lastName} </Link>
    </td>
    <td>{user.points}</td>
  </tr>
);

// Require a document to be passed to this component.
UserPointsItem.propTypes = {
  user: PropTypes.shape({
    firstName: PropTypes.string,
    lastName: PropTypes.string,
    points: PropTypes.number,
    image: PropTypes.string,
    _id: PropTypes.string,
  }).isRequired,
  // eslint-disable-next-line react/require-default-props
  rank: PropTypes.number,
};

export default UserPointsItem;
````
````
/* Renders a table containing all of the Profile documents to display point leaderboard. Use <UserPointsItem> to render each row. */
const ListProfiles = () => {
  // useTracker connects Meteor data to React components. https://guide.meteor.com/react.html#using-withTracker
  const { ready, profiles } = useTracker(() => {
    // Note that this subscription will get cleaned up
    // when your component is unmounted or deps change.
    // Get access to Profiles documents.
    const subscription = Meteor.subscribe(Profiles.userPublicationName);
    // Determine if the subscription is ready
    const rdy = subscription.ready();
    // Get the Profile documents
    const profileItems = Profiles.collection.find({}, { sort: { points: -1 } }).fetch();
    return {
      profiles: profileItems,
      ready: rdy,
    };
  }, []);
````

This project significantly enhanced my software development and collaboration skills, akin to my previous experience with the Club Hub project in 2023. It provided invaluable lessons in taking initiative within a team setting. I also learned how to establish effective coordination strategies, how to maintain regular communication to streamline development, and the importance of setting appropriate goals to meet weekly milestones and deadlines. Working collaboratively on milestones taught me to leverage team strengths and manage workload distribution effectively. Additionally, I gained insights into the process of adding new project features and optimizing code for future scalability.

[GitHub project repo](https://github.com/mongo-mongoers/club-hub)
