<template>
  	<div>
  		<router-link 
  			to="/time-entries/log-time" v-if="$route.path == '/time-entries'" class="btn btn-primary">	
  			创建
  		</router-link>

  		<div v-if="$route.path == '/time-entries/log-time'">
  			<h3>创建</h3>
  		</div>

  		<hr>

  		<router-view></router-view>

		<div class="time-entries">
      		<p v-if="!plans.length"><strong>还没有任何计划</strong></p>

		    <div class="list-group">
		        <a class="list-group-item" v-for="(plan,index) in plans">
		          	<div class="row">
			            <div class="col-sm-2 user-details">
			              	<img :src="plan.avatar" class="avatar img-circle img-responsive" />
			              	<p class="text-center">
			                	<strong>
			                  		{{ plan.name }}
			                	</strong>
			              	</p>
			            </div>

		            	<div class="col-sm-2 text-center time-block">
			              	<h3 class="list-group-item-text total-time">
			                	<i class="glyphicon glyphicon-time"></i>
			                	{{ plan.totalTime }}
			              	</h3>
			              	<p class="label label-primary text-center">
			                	<i class="glyphicon glyphicon-calendar"></i>
			                	{{ plan.date }}
			              	</p>
		            	</div>

		            	<div class="col-sm-7 comment-section">
		              		<p>{{ plan.comment }}</p>
		            	</div>

	            		<div class="col-sm-1">
		              		<button
		                	class="btn btn-xs btn-danger delete-button"
		                	@click="deletePlan(index)">
	              			X
		              		</button>
		            	</div>

		          </div>
		        </a>
		    </div>
    	</div>
  	</div>
</template>
<script>
	export default {
      	name : 'TimeEntries',
    	computed : {
    		plans () {
            	return this.$store.state.list
          	}
    	},
    	methods : {
    		deletePlan(index) {
    			// 减去总时间
	            this.$store.dispatch('decTotalTime',this.plans[index].totalTime)
	            // 删除该计划
	            this.$store.dispatch('deletePlan',index)
    		}
    	}
    }
</script>