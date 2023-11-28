package main

import (
	"context"
	"fmt"
	"log"
	"os"
	"strconv"
	"github.com/shomali11/slacker"
)

func printCommandsEvents(analyticsChannel <- chan *slacker.CommandEvent)  {
	for event := range analyticsChannel {
		fmt.Println("Command Events")
		fmt.Println(event.Timestamp)
		fmt.Println(event.Command)
		fmt.Println(event.Parameters)
		fmt.Println(event.Event)
		fmt.Println()

	}
}

func main(){
	os.Setenv("SLACK-BOT-TOKEN","xoxb-6274375252304-6248625836485-QQOTkqFblI1Kumb5A0tMEnlh")
	os.Setenv("SLACK-APP-TOKEN","xapp-1-A066YUFFMF1-6274490920784-78b0645db2e61ea032f9fa42b6c24d123027938fe66fd973cf6f6963d4e47ad9")

	bot := slacker.NewClient(os.Getenv("SLACK-BOT-TOKEN"),os.Getenv("SLACK-APP-TOKEN"))
	
	go printCommandsEvents(bot.CommandEvents())

	bot.Command("my yob is <year>",&slacker.CommandDefinition{
		Description: "yob calculator",
		// Example: "my yob is 2020",
		Handler: func (botCtx slacker.BotContext,request slacker.Request,response slacker.ResponseWriter)  {
			year := request.Param("year") 
			yob,err := strconv.Atoi(year)
			if err != nil{
				println("error")
			}
			age := 2023-yob
			r := fmt.Sprintf("age is %d",age)
			response.Reply(r)
		},
		
	})

	ctx,cancel := context.WithCancel(context.Background())
	defer cancel()
	
	err := bot.Listen(ctx)
	if err != nil{
		log.Fatal(err)
	}
}