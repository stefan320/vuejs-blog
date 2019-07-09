<template >
  <div class="comments__section" v-if="!visable.show">
    <h1 class="header">Comments</h1>
    <div v-for="comment in articleInfo.comments" :id="comment.id" :key="comment.id" class="comment">
      <h2 class="header-secondary text--blue capitalize">{{comment.author}}</h2>
      <p class="paragraph">{{comment.text | noComments}}</p>
      <button v-if="comment.text" class="btn btn--danger" @click.stop="deleteComment">Delete Comment</button>
    </div>
    <div v-on:click.stop class="comments--user">
      <h1 class="header">Add Comment</h1>
      <form action>
        <input type="text" class="input" placeholder="Name" v-model="newCommentAuthor" required />
        <textarea class="input" v-model="userComment" placeholder="Comment"></textarea>
        <button class="btn btn--success" @click.prevent="newComment">Post Comment</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  props: ["articleInfo", "visable", "index"],
  filters: {
    noComments: value => {
      if (!value) {
        value = "No comments available.";
      }
      return value;
    }
  },
  data() {
    //Every blog has a new data function
    return {
      newCommentAuthor: "",
      userComment: "",
      commentIDS: []
    };
  },
  methods: {
    // Check if inputs are valid
    newComment(event) {
      if (this.inputValidation()) {
        this.articleInfo.comments.push({
          author: this.newCommentAuthor,
          text: this.userComment,
          id: this.updateCommentIDS()
        });
      }
      //Clear Input Fields
      this.newCommentAuthor = "";
      this.userComment = "";
    },
    inputValidation(el) {
      if (!this.newCommentAuthor) {
        alert("Name cannot be empty!");
        return false;
      }
      if (!this.userComment) {
        alert("Comment cannot be empty!");
        return false;
      } else {
        return true;
      }
    },

    updateCommentIDS() {
      const newID = Math.floor(Math.random() * 1000000);
      this.commentIDS.push(newID);
      return newID;
    },

    // Iterrate through comments Array IDS until finding one that matches the id of the comment div that needs to be deleted
    // use splice on the comments array ro delete the comment that need to be deleted
    deleteComment(event) {
      for (let i in this.articleInfo.comments) {
        if (
          parseInt(this.articleInfo.comments[i].id) ===
          parseInt(event.target.parentElement.id)
        ) {
          this.articleInfo.comments.splice(i, 1);
          break;
        }
      }
    }
  },
  created() {
    //Loop Through all comments array and If there are any comments push its  id to commentIDS
    // console.log(this.commentIDS);
    this.articleInfo.comments.forEach(el => {
      if (el.id) {
        this.commentIDS.push(JSON.parse(el.id));
      }
    });
  }
};
</script>

<style>
.comments__section {
  margin: 2rem 0;
  background-color: #fefefe;
}
.comment {
  padding: 1rem 0;
}
.input {
  display: block;
  border: none;
  border: 1px solid #52616a;

  padding: 0.5rem 0;
  border-radius: 2px;
  width: 100%;
  margin: 1.2rem 0;
}

.text--blue {
  color: #1e2022;
}
.btn {
  display: block;
  font-size: 1.4rem;
  font-weight: 600;
  background-color: transparent;
  cursor: pointer;
  margin: 0;
}
.btn--danger {
  border: none;
  padding: 0.33rem 0;
  color: #c21e25;
  transition: all 0.3s;
}
.btn--success {
  border: 1px solid #52616a;
  color: #52616a;
  transition: all 0.3s;
  padding: 1rem;
}

.btn--success:hover {
  outline: transparent;
  color: #f0f5f9;
  background-color: #52616a;
}

.btn--danger:hover {
  text-decoration: underline;
}
</style>
